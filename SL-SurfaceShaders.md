# Writing Surface Shaders

|**5.6 DRAFT ADDITION TO DOCUMENTATION** |
|:---|
|This feature has additional or changed functionality in Unity 5.6. The link below is first draft document of that addition or change. As such, the information in this document may be subject to change before final release.<br/><br/>See first draft [Light Modes](https://docs.google.com/document/d/116JvLXljfbdfllOLlyzVvWmNWpbUwcYKV16blVHuS2E/edit) documentation.|


Writing shaders that interact with lighting is complex. There are different light types, different shadow options, different rendering paths (forward and deferred rendering), and the shader should somehow handle all that complexity.

__Surface Shaders__ in Unity is a code generation approach that makes it much easier to write lit shaders than using low level [vertex/pixel shader programs](SL-ShaderPrograms). Note that there are no custom languages, magic or ninjas involved in Surface Shaders; it just generates all the repetitive code that would have to be written by hand. You still write shader code in HLSL.

For some examples, take a look at [Surface Shader Examples](SL-SurfaceShaderExamples) and [Surface Shader Custom Lighting Examples](SL-SurfaceShaderLightingExamples).



## How it works


You define a "surface function" that takes any UVs or data you need as input, and fills in output structure `SurfaceOutput`. SurfaceOutput basically describes _properties of the surface_ (it's albedo color, normal, emission, specularity etc.). You write this code in HLSL.

Surface Shader compiler then figures out what inputs are needed, what outputs are filled and so on, and generates actual [vertex&pixel shaders](SL-ShaderPrograms), as well as rendering passes to handle forward and deferred rendering.

Standard output structure of surface shaders is this:

````
struct SurfaceOutput
{
    fixed3 Albedo;	// diffuse color
    fixed3 Normal;	// tangent space normal, if written
    fixed3 Emission;
    half Specular;	// specular power in 0..1 range
    fixed Gloss;	// specular intensity
    fixed Alpha;	// alpha for transparencies
};
````

In Unity 5, surface shaders can also use physically based lighting models. Built-in Standard and StandardSpecular lighting models (see below) use these output structures respectively:

````
struct SurfaceOutputStandard
{
	fixed3 Albedo;		// base (diffuse or specular) color
	fixed3 Normal;		// tangent space normal, if written
	half3 Emission;
	half Metallic;		// 0=non-metal, 1=metal
	half Smoothness;	// 0=rough, 1=smooth
	half Occlusion;		// occlusion (default 1)
	fixed Alpha;		// alpha for transparencies
};
struct SurfaceOutputStandardSpecular
{
	fixed3 Albedo;		// diffuse color
	fixed3 Specular;	// specular color
	fixed3 Normal;		// tangent space normal, if written
	half3 Emission;
	half Smoothness;	// 0=rough, 1=smooth
	half Occlusion;		// occlusion (default 1)
	fixed Alpha;		// alpha for transparencies
};
````


## Samples


See [Surface Shader Examples](SL-SurfaceShaderExamples), [Surface Shader Custom Lighting Examples](SL-SurfaceShaderLightingExamples) and [Surface Shader Tessellation](SL-SurfaceShaderTessellation) pages.


## Surface Shader compile directives


Surface shader is placed inside `CGPROGRAM..ENDCG` block, just like any other shader. The differences are:

* It must be placed inside [SubShader](SL-SubShader) block, not inside [Pass](SL-Pass). Surface shader will compile into multiple passes itself.
* It uses `#pragma surface ...` directive to indicate it's a surface shader.

The `#pragma surface` directive is:

    #pragma surface surfaceFunction lightModel [optionalparams]


### Required parameters

* surfaceFunction - which Cg function has surface shader code. The function should have the form of `void surf (Input IN, inout SurfaceOutput o)`, where Input is a structure you have defined. Input should contain any texture coordinates and extra automatic variables needed by surface function.
* lightModel - lighting model to use. Built-in ones are physically based `Standard` and `StandardSpecular`, as well as simple non-physically based `Lambert` (diffuse) and `BlinnPhong` (specular). See [Custom Lighting Models](SL-SurfaceShaderLighting) page for how to write your own.
	* `Standard` lighting model uses `SurfaceOutputStandard` output struct, and matches the Standard (metallic workflow) shader in Unity.
	* `StandardSpecular` lighting model uses `SurfaceOutputStandardSpecular` output struct, and matches the Standard (specular setup) shader in Unity.
	* `Lambert` and `BlinnPhong` lighting models are not physically based (coming from Unity 4.x), but the shaders using them can be faster to render on low-end hardware.


### Optional parameters

**Transparency and alpha testing** is controlled by `alpha` and `alphatest` directives. Transparency
can typically be of two kinds: traditional alpha blending (used for fading objects out) or more
physically plausible "premultiplied blending" (which allows semitransparent surfaces to retain proper
specular reflections). Enabling semitransparency makes the generated surface shader code contain
[blending](SL-Blend) commands; whereas enabling alpha cutout will do a fragment discard in the
generated pixel shader, based on the given variable.

* `alpha` or `alpha:auto` - Will pick fade-transparency (same as `alpha:fade`) for simple lighting functions, and premultiplied transparency (same as `alpha:premul`) for physically based lighting functions.
* `alpha:blend` - Enable alpha blending.
* `alpha:fade` - Enable traditional fade-transparency.
* `alpha:premul` - Enable premultiplied alpha transparency.
* `alphatest:VariableName` - Enable alpha cutout transparency. Cutoff value is in a float variable with VariableName. You'll likely also want to use `addshadow` directive to generate proper shadow caster pass.
* `keepalpha` - By default opaque surface shaders write 1.0 (white) into alpha channel, no matter what's output in the Alpha of output struct or what's returned by the lighting function. Using this option allows keeping lighting function's alpha value even for opaque surface shaders.
* `decal:add` - Additive decal shader (e.g. terrain AddPass). This is meant for objects that lie atop of other surfaces, and use additive blending. See [Surface Shader Examples](SL-SurfaceShaderExamples)
* `decal:blend` - Semitransparent decal shader. This is meant for objects that lie atop of other surfaces, and use alpha blending. See [Surface Shader Examples](SL-SurfaceShaderExamples)


**Custom modifier functions** can be used to alter or compute incoming vertex data, or to
alter final computed fragment color.

* `vertex:VertexFunction` - Custom vertex modification function. This function is invoked at start of generated vertex shader, and can modify or compute per-vertex data. See [Surface Shader Examples](SL-SurfaceShaderExamples).
* `finalcolor:ColorFunction` - Custom final color modification function. See [Surface Shader Examples](SL-SurfaceShaderExamples).
* `finalgbuffer:ColorFunction` - Custom deferred path for altering gbuffer content.
* `finalprepass:ColorFunction` - Custom prepass base path.

**Shadows and Tessellation** - additional directives can be given to control how shadows and tessellation is handled.

* `addshadow` - Generate a shadow caster pass. Commonly used with custom vertex modification, so that shadow casting also gets any procedural vertex animation. Often shaders don't need any special shadows handling, as they can just use shadow caster pass from their fallback.
* `fullforwardshadows` - Support all light shadow types in [Forward](RenderTech-ForwardRendering) rendering path. By default shaders only support shadows from one directional light in forward rendering (to save on internal shader variant count). If you need point or spot light shadows in forward rendering, use this directive.
* `tessellate:TessFunction` - use DX11 GPU tessellation; the function computes tessellation factors. See [Surface Shader Tessellation](SL-SurfaceShaderTessellation) for details.


**Code generation options** - by default generated surface shader code tries to handle all possible
lighting/shadowing/lightmap scenarios. However in some cases you know you won't need some of them, and it is possible
to adjust generated code to skip them. This can result in smaller shaders that are faster to load.

* `exclude_path:deferred`, `exclude_path:forward`, `exclude_path:prepass`  - Do not generate passes for given rendering path ([Deferred Shading](RenderTech-DeferredShading), [Forward](RenderTech-ForwardRendering) and [Legacy Deferred](RenderTech-DeferredLighting) respectively).
* `noshadow` - Disables all shadow receiving support in this shader.
* `noambient` - Do not apply any ambient lighting or light probes.
* `novertexlights` - Do not apply any light probes or per-vertex lights in Forward rendering.
* `nolightmap` - Disables all lightmapping support in this shader.
* `nodynlightmap` - Disables runtime dynamic global illumination support in this shader.
* `nodirlightmap` - Disables directional lightmaps support in this shader.
* `nofog` - Disables all built-in Fog support.
* `nometa` - Does not generate a "meta" pass (that's used by lightmapping & dynamic global illumination to extract surface information).
* `noforwardadd` - Disables [Forward](RenderTech-ForwardRendering) rendering additive pass. This makes the shader support one full directional light, with all other lights computed per-vertex/SH. Makes shaders smaller as well.
* `nolppv` - Disables Light Probe Proxy Volume support in this shader.


**Miscellaneous options**

* `softvegetation` - Makes the surface shader only be rendered when Soft Vegetation is on.
* `interpolateview` - Compute view direction in the vertex shader and interpolate it; instead of computing it in the pixel shader. This can make the pixel shader faster, but uses up one more texture interpolator.
* `halfasview` - Pass half-direction vector into the lighting function instead of view-direction. Half-direction will be computed and normalized per vertex. This is faster, but not entirely correct.
* `approxview` - Removed in Unity 5.0. Use `interpolateview` instead.
* `dualforward` - Use [dual lightmaps](GIIntro) in [forward](RenderTech-ForwardRendering) rendering path.


To see what exactly is different from using different options above, it can be helpful to use "Show Generated Code" button in the [Shader Inspector](class-Shader).


## Surface Shader input structure


The input structure `Input` generally has any texture coordinates needed by the shader. Texture coordinates must be named "`uv`" followed by texture name (or start it with "`uv2`" to use second texture coordinate set).

Additional values that can be put into Input structure:

* `float3 viewDir` - contains view direction, for computing Parallax effects, rim lighting etc.
* `float4` with `COLOR` semantic - contains interpolated per-vertex color.
* `float4 screenPos` - contains screen space position for reflection or screenspace effects. Note that this is not suitable for [GrabPass](SL-GrabPass); you need to compute custom UV yourself using `ComputeGrabScreenPos` function.
* `float3 worldPos` - contains world space position.
* `float3 worldRefl` - contains world reflection vector _if surface shader does not write to o.Normal_. See Reflect-Diffuse shader for example.
* `float3 worldNormal` - contains world normal vector _if surface shader does not write to o.Normal_.
* `float3 worldRefl; INTERNAL_DATA` - contains world reflection vector _if surface shader writes to o.Normal_. To get the reflection vector based on per-pixel normal map, use `WorldReflectionVector (IN, o.Normal)`. See Reflect-Bumped shader for example.
* `float3 worldNormal; INTERNAL_DATA` - contains world normal vector _if surface shader writes to o.Normal_. To get the normal vector based on per-pixel normal map, use `WorldNormalVector (IN, o.Normal)`.


## Surface Shaders and DirectX 11 HLSL syntax


Currently some parts of surface shader compilation pipeline do not understand [DirectX 11](UsingDX11GL3Features)-specific HLSL syntax, so if you're using HLSL features like StructuredBuffers, RWTextures and other non-DX9 syntax, you have to wrap it into a DX11-only preprocessor macro.

See [Platform Specific Differences](SL-PlatformDifferences) and [Shading Language](SL-ShadingLanguage) pages for details.
