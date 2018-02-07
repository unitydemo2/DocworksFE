# Scriptable render pipeline

*Note: This is an experimental feature.*

The scriptable render pipeline is not supplied with the standard Unity Editor installer which you download from the [Unity store](https://store.unity.com/). Instead, download the scriptable render pipeline from [the Unity Technologies GitHub](https://github.com/Unity-Technologies/ScriptableRenderLoop) and install it separately.

This page contains:

* [The motivation behind the feature](#Motivation)
* [The new built-in "HD Render Loop"](#Built-in)
* [API overview](#APIOverview)
* [Appendix - current rendering pipeline in Unity](#Appendix)



**Feature summary**

Reimagine the rendering pipeline to support more flexibility and transparency. The main Unity rendering pipeline will be replaced by multiple "Render Loops", built in C# on a C++ foundation. The C# code for the "Render Loops" will be open-sourced on GitHub, enabling users to investigate, enhance, or create their own custom render loops.

<a name="Motivation"></a>
### The motivation behind the feature

Current Unity’s rendering pipeline is described in [Appendix - Current Rendering Pipeline](#Appendix). There are several improvements we want to make -- the major ones are spelled below.

#### Need to perform better on modern hardware

Both "one light per draw call" forward rendering, and “stencil mark + draw shape per light” deferred shading are not exactly modern approaches -- they were fine for roughly DX9 hardware, but with advent of compute shaders generally we can do much better. Our forward shading suffers from too many draw calls (CPU + vertex transform cost) and bandwidth consumed by repeated sampling of surface textures & blending; whereas deferred shading suffers from draw call count, not enough light culling, cost of doing stencil mark + draw call per light and repeated fetching of G-buffer data. Additionally, on tile-based GPUs it does tile store+load too much when realtime shadows are involved, and does not take advantage of tile storage or framebuffer fetch.

We’d like to ship Unity with an out-of-the box rendering pipeline that is targeted at modern hardware -- where we can rely on API & GPU features like compute shaders, draw call instancing, constant buffers etc.

#### Easier to customize & extend, less "black box"

Most of Unity users would probably not modify the built-in rendering pipeline, but some of the more advanced teams *do* want to modify or extend it. So it has to be extensible and much less opaque than today.

While the current rendering pipeline is *somewhat* extensible (users can write their own shaders, manually control camera rendering, change settings, extend the rendering pipeline with [command buffers](GraphicsCommandBuffers)), it is not extensible enough. Additionally, it is too much of a "black box", and while the documentation, conference presentations, MIT-licensed built-in shader source code and community knowledge does fill in the gaps, some parts are hard to understand without a Unity source code license. We want all the high level code and shader/compute code to be a MIT-licensed open source project, similar to how [Post-Processing](PostProcessingOverview), [UI](https://bitbucket.org/Unity-Technologies/ui) or [Networking](https://bitbucket.org/Unity-Technologies/networking) already are.

A "single render pipeline for everything" likely has some compromises that make it more flexible at expense of performance. We imagine that, for example, these kinds of rendering pipelines would make sense in many cases:

* Optimized for modern PC/console (DX11 baseline, "high end" graphics).

* Optimized for on-tile storage of mobile GPUs, using framebuffer fetch or other available techniques.

* Optimized for VR (e.g. forward shading + MSAA, single-pass rendering, caching/sharing eye rendering results in distance, various schemes of viewport/resolution stitching).

* Optimized for low-end devices (old mobile, old PC) or simple 2D games: simple one pass lighting (limited # of lights, and/or vertex lighting).

These don’t have to be physically separate rendering pipelines, could be options in some other existing pipelines.

#### Easier dealing with backwards compatibility

This is a hard problem for us at Unity R&D, basically doing big changes to how the rendering engine works is quite hard -- mostly because people do expect to update to a more recent Unity version and have things "still working as they did". Except when they don’t, i.e. they actively want new changes... For example, we changed Standard shader from Blinn-Phong to GGX specular in Unity 5.3 -- mostly this is a good thing, except for people who were mid-production and now their specular behaves differently (so they probably have to re-tweak their lighting setups and materials).

We’re thinking, that *if* the high level structure of the rendering code, and all the shader code, was easily "forkable" and versionable, then this problem could become easier.

#### Scriptable render loops: the new foundation

We think all or most of the problems listed above can be solved fairly elegantly by having a solid, orthogonal, performant foundation to build upon, which would basically be "an ability to render sets of objects with various filtering criteria efficiently". The division of work would be:

| Unity C++ code | C#/shader code (MIT open source) |
|:---|:---| 
| Culling<br/> Render set of objects with filter/sort/params<br/> Internal graphics platform abstraction | Camera setup<br/> Light setup <br/> Shadows setup <br/> Frame render pass structure & logic <br/>Shader/compute code |

The C++ side would be mostly not even aware that things like "Camera" or “Light” exist; e.g. culling code gets arrays of bounding primitives and matrices / culling planes as input. It does not care whether it’s culling main view, reflection rendering view or a shadow map view.

Likewise, rendering code is expressed in terms of "from the culling results, render everything that is within opaque render queues range, has this shader pass and does not have that shader pass, sort by material then by distance, setup light probe constants per-object". There is *some *amount of conventions and built-in things in there, mostly in what kind of data should be set as per-instance data for each object (light probes, reflection probes, lightmaps, per-object light lists etc.).

There’s a lot of underlying platform graphics abstraction changes that we’re doing in order to be able to provide a robust, high performance and orthogonal set of "building blocks" to build scriptable render loops upon, but they are mostly outside of the scope of this document. Some of the changes worked on are:

* Expose "Buffer" as a C# class, that would be used for all kinds of buffer data (vertices, indices, uniforms, compute data etc.). Ability to create and manually update uniform/constant buffers from C# side.

* Compute shader related improvements, particularly how data is passed to them.

* Remove split between TextureFormat and RenderTextureFormat, have something like "DataFormat" instead that is used in all graphics related code (similar to DXGI formats on D3D). Expose more formats than today.

* Asynchronous readbacks of GPU data. Asynchronous compute.

<br/>
<a name="APIOverview"></a>
## API overview

Note: the API is in flux, and this document might not be exact wrt whatever Unity version you’re testing with right now.

The main entry point is RenderLoop.renderLoopDelegate, which is in a form of
	bool PrepareRenderLoop(Camera[] cameras, RenderLoop outputLoop);

When the render loop delegate is registered, then all rendering goes into that function, and the existing built-in rendering loops are *not executed* at all.

Inside of the render loop delegate, typically it would do culling for all the cameras (via the new CullResults class), and then do series of calls to RenderLoop.DrawRenderers intermixed with CommandBuffer calls to setup global shader properties, change render targets, dispatch compute shaders etc.

Overall, the design is that the C# render loop code has full control over per-camera logic (it gets all cameras as input), and all per-light logic (it gets all visible lights as a culling result), but generally does not do per-object logic. Objects are rendered in "sets" -- DrawRenderers call that specifies which subset of visible objects to render, how to sort them, and what kind of per-object data to setup.

The simplest possible render loop would look something like this:

```
public bool __Render__(Camera[] cameras, RenderLoop renderLoop)
{
    foreach (var camera in cameras)
    {
        // cull a camera
        CullResults cull;
        CullingParameters cullingParams;
        if (!CullResults.GetCullingParameters (camera, out cullingParams))
            continue;
        cull = __CullResults.Cull__ (ref cullingParams, renderLoop);
        renderLoop.SetupCameraProperties (camera);
        // setup render target and clear it
        var cmd = new CommandBuffer();
        cmd.SetRenderTarget(BuiltinRenderTextureType.CameraTarget);
        cmd.ClearRenderTarget(true, true, Color.black);
        renderLoop.__ExecuteCommandBuffer__(cmd);
        cmd.Dispose();
        // draw all the opaque objects using ForwardBase shader pass
        var settings = new __DrawRendererSettings__(cull, camera, "ForwardBase");
        settings.sorting.sortOptions = SortOptions.SortByMaterialThenMesh;
        settings.inputFilter.SetQueuesOpaque();
        renderLoop.__DrawRenderers__(ref settings);
        renderLoop.Submit ();
    }
    return true;
}
```

Most important new scripting APIs:

```
// main entry point
struct RenderLoop
{
	void ExecuteCommandBuffer (CommandBuffer);
	void DrawRenderers (ref DrawRendererSettings);
	void DrawShadows (ref DrawShadowsSettings); // similar, slightly specialized
	void DrawSkybox (Camera);
	static PrepareRenderLoop renderLoopDelegate;
}
// Setup and control how sets of objects are rendered by RenderLoop.DrawRenderers
struct DrawRendererSettings
{
	DrawRendererSortSettings sorting;
	ShaderPassName shaderPassName;
	InputFilter inputFilter;
	RendererConfiguration rendererConfiguration;
	CullResults cullResults { set };
}
struct DrawRendererSortSettings
{
Matrix4x4 worldToCameraMatrix;
Vector3 cameraPosition;
SortOptions sortOptions;
	bool sortOrthographic;
}
enum SortOptions { None, FrontToBack, BackToFront, SortByMaterialThenMesh, ... };
struct InputFilter
{
	int renderQueueMin, renderQueueMax;
	int layerMask;
};
// what kind of data should be set up per-object when rendering them
[Flags] enum RendererConfiguration
{
	None,
	PerObjectLightProbe,
	PerObjectReflectionProbes,
	PerObjectLightProbeProxyVolume,
	PerObjectLightmaps,
	ProvideLightIndices,
	// ...
};
// Culling and cull results
struct CullResults
{
	VisibleLight[] visibleLights;
	VisibleReflectionProbe[] visibleReflectionProbes;
	bool GetCullingParameters(Camera, out CulingParameters);
	static CullResults Cull(ref CullingParameters, RenderLoop renderLoop);
	// utility functions, like
// ComputeDirectionalShadowMatricesAndCullingPrimitives etc
}
struct CullingParameters
{
	int isOrthographic;
	LODParameters lodParameters;
	Plane cullingPlanes[10];
	int cullingPlaneCount;
	int cullingMask;
	float layerCullDistances[32];
	Matrix4x4 cullingMatrix;
	Vector3 position;
	float shadowDistance;
ReflectionProbeSortOptions reflectionProbeSortOptions;
Camera camera;
}
struct VisibleLight
{
	LightType lightType;
	Color finalColor;
	Rect screenRect;
	Matrix4x4 localToWorld;
	Matrix4x4 worldToLocal;
	float range;
	float invCosHalfSpotAngle;
	VisibleLightFlags flags;
	Light light { get }
}

struct VisibleReflectionProbe; // similar to VisibleLight…
```

The API outlined above is *very much not final!* Things that are very likely to change:

* Considering an option to not have RenderLoop class, but instead have CommandBuffer contain functions like DrawRenderers etc., and possibly have nested command buffers too.

* Culling API changes to enable more performance, i.e. jobified culling overlapping with other work.

* Possibly more renderer filtering options.

* More explicit "render pass" controls, instead of current “set render target” API.

#### Usage, inner workings, performance

The general flow is that your own render loop code is responsible for culling, and for rendering everything. Including setting up per-frame or per-renderpass shader uniform variables, managing temporary render targets and setting them up, dispatching compute shaders etc.

Visible lights and probes can be queried from the cull results, and for example their information put into compute shader buffers for tiled light culling. Alternatively, the render loop provides several ways of setting up per-object light lists for DX9-style forward rendering.

On the CPU performance side, the API is built in a way where there’s generally no *per-object* operations going on -- the C# side of the code is independent of the scene complexity. It typically loops over cameras, and does some iteration over visible lights to either render shadows, or to pack light data for shader usage. The rest of code that is written in C# is setting up render passes / render textures, and issuing "draw this subset of visible objects" commands.

The C++ part of code (culling, DrawRenderers, DrawShadows) is written in a high-performance style that generally just goes over tightly packed data arrays, and is internally multithreaded. Our current experiments show that with this split (high level frame setup in C#, culling/rendering in C++) we can get same or even better performance of our previous rendering loop implementations.

The C# side looks like it would create a lot of garbage-collected objects; we are looking into ways of exposing "native" (C++ side) data directly to C# without extra round-trips; in C# that would look very similar to an array that writes directly into native side memory. This is a somewhat separate topic, which we’ll talk about separately.



<br/>
<a name="Built-in"></a>
## New built-in "HD Render Loop"

We plan to provide a built-in "HD Render Loop" targeted at modern (compute-capable) platforms. Currently it is developed with PC and PS4/XB1 consoles in mind, but we’ll be looking at optimizing it for high-end mobile platforms too. Of particular interest for mobile is optimizing it for on-tile storage / framebuffer fetch and other bandwidth-saving techniques.

Internally, shaders are written in a way that is less reliant on separate shader variants for every imaginable knob, and more using "static" (uniform based) branching, with shader variant specializations only used where that makes sense based on shader analysis / profiling on modern GPUs.

The new HDRenderLoop is being developed at [__github ScriptableRenderLoop__](https://github.com/Unity-Technologies/ScriptableRenderLoop) (might be messy at any point, only use if you’re super-curious right now).

#### Lighting Features

* Tiled light culling with compute shaders:

    * Fine pruned tiled lighting ([FPTL](http://mmikkelsen3d.blogspot.lt/2016/05/fine-pruned-tiled-lighting.html)) for deferred shaded opaque objects.

    * Clustered tiled lighting for forward-rendered objects and transparencies.

    * Rendering can be switched between deferred and forward, depending on what is better for the project.

* Lights:

    * Usual punctual (point/spot) and directional lights.

    * Area lights ([polygonal lights](https://eheitzresearch.wordpress.com/415-2/) and line lights).

    * Correct linear lighting & PBR.

    * Physical light units, IES lights.

    * *(Later)* Frustum lights (i.e. bounded directional light).

* Shadows:

    * All realtime shadows are suballocated from a single atlas.

    * Intuitive controls over shadow memory budget and per-light resolution overrides.

    * Better PCF filtering, particularly for spot/point lights.

    * Shadows on semitransparent objects.

* GI:

    * Correct HDR.

    * Consistency with direct illumination.

* *(Later) *Improved Shadows

    * Exponential shadow maps (ESM/EVSM).

    * Improved shadows for area lights.

* *(Later)* Volumetric Lighting

    * Sky/fog atmospheric scattering model.

    * Local fog.

#### Material features

* GGX with Metal & Specular parametrizations, similar to current Standard shader.

* Anisotropic GGX (Metal parametrization)

* Sub-surface scattering & transmission

* Clear coat

* Double sided support

* Good specular occlusion

* Layered materials (mix & mask inputs of other materials, with up to 4 layers)

* Heightmaps either via parallax or displacement tessellation

* *(later)* Built-in LOD cross-fade / dithering

* *(later)* Hair, Eye, Cloth shading models

#### Camera features

* Physically based camera parameters

* Support for Unity’s [PostProcessing stack](PostProcessing-Stack)

* Distortion

* Velocity buffer (for motion blur / temporal AA)

* *(later) *Half/quarter resolution rendering (e.g. for particles) and compositing.

#### Workflow / debug features

* Views of shader inputs (albedo, normals etc.)

* Views of all intermediate buffers of rendering (lighting, motion vectors etc.)

* Debug menu to control rendering of various passes

<br/>
<a name="Appendix"></a>
## Appendix - current rendering pipeline in Unity

Currently (Unity 5.5 and earlier) Unity supports two rendering pipelines for scene (forward rendering and deferred shading), and one way to render realtime shadows. Following is the description of the current pipeline in more detail:

#### Shadows

Shadowing system mostly works the same no matter whether the forward or deferred shading is used.

* Each realtime light with shadows enabled gets a separate shadow map.

* Shadow maps are traditional depth texture maps, in shaders sampled with PCF filtering (no VSM/EVSM etc. shadows).

* Directional lights can use cascaded shadow maps (2 or 4 cascades); the shadow map space is divided into cascades like in an atlas.

* Spot lights always use simple 2D shadowmap; point lights use a cubemap.

* Shadowmap size is computed based on quality settings, screen resolution and light’s projection size on screen; or can be controlled by game developer explicitly from scripts per-light.

* Cascaded shadow maps are applied in "screen space" -- there’s a separate “gather and do PCF filtering” step that produces screenspace shadow mask texture; later on regular object rendering just does one sample into this texture.

* No support for receiving shadows onto semitransparent objects.

#### Forward rendering

The default mode of operation is largely DX9-style "one draw call per light with additive blending". Quality settings of the game determine how many lights per-object will be rendered in realtime; the rest are folded into a spherical harmonics (SH) representation and rendered together with other ambient lighting.

* Optionally before main scene rendering: a "depth texture" rendering pass. This kicks in if scripts require it, or other features (e.g. realtime cascaded shadows) need it. Conceptually this is similar to Z-prepass; produces a texture with scene depth buffer.

* Optionally before main scene rendering: a "motion vectors" rendering pass. This kicks in if scripts (e.g. motion blur or temporal AA) require it. Renders a texture of velocity vectors for objects that need them.

* Realtime shadow maps are rendered before main scene rendering; all shadows are in memory at once.

* Actual scene rendering pass specialized in two shader sets: "ForwardBase" (ambient/probes + lightmaps + lighting/shadows from main directional light), followed by additive blending “ForwardAdd”, that does realtime lighting one light at a time.

#### Deferred shading

This is "traditional" DX9-style deferred shading: G-buffer rendering pass, followed by “render light shapes one by one” pass where each of them reads G-buffer data, computes illumination and adds it into lighting buffer.

* Similar to forward rendering, an optional motion vectors pass before the G-buffer.

* [Reflection probes](class-ReflectionProbe) are rendered one by one similar to lights, by rendering box shapes and adding reflections into a texture.

* Lights are rendered one by one, by rendering light shapes (fullscreen quad or sphere or cone) and adding reflections into a texture.

* Shadow map for a light is rendered just before rendering each light, and generally discarded right after done with it.

* Stencil marking is used for both lights and reflection probes to limit the amount of pixels actually computed.

* Objects that don’t support deferred shading, and all semitransparent objects, are rendered using forward rendering.

#### Customization

It is possible to customize the above behavior to some extent, but not much. For example, Valve’s The Lab Renderer (on [Asset Store](https://www.assetstore.unity3d.com/en/#!/content/63141)) replaces the built-in behavior by (purely in C# + shaders):

* Implementing a custom shadows system, where all shadows are packed into one atlas.

* Custom forward rendering system, where all lights are rendered in one pass; light information is setup into custom shader uniform variables.

<br/><br/>

---

* <span class="page-edit"> 2017-05-26  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">New feature in 5.6</span>
