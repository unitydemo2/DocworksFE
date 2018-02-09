# Deferred shading rendering path

|**5.6 DRAFT ADDITION TO DOCUMENTATION** |
|:---|
|This feature has additional or changed functionality in Unity 5.6. The link below is first draft document of that addition or change. As such, the information in this document may be subject to change before final release.<br/><br/>See first draft [Light Modes](https://docs.google.com/document/d/116JvLXljfbdfllOLlyzVvWmNWpbUwcYKV16blVHuS2E/edit) documentation.|

This page details the deferred shading [rendering path](RenderingPaths). See [Wikipedia: deferred shading](http://en.wikipedia.org/wiki/Deferred_shading) for an introductory technical overview.

## Overview

When using deferred shading, there is no limit on the number of lights that can affect a GameObject. All lights are evaluated per-pixel, which means that they all interact correctly with normal maps, etc. Additionally, all lights can have cookies and shadows.

Deferred shading has the advantage that the processing overhead of lighting is proportional to the number of pixels the light shines on. This is determined by the size of the light volume in the Scene regardless of how many GameObjects it illuminates. Therefore, performance can be improved by keeping lights small. Deferred shading also has highly consistent and predictable behaviour. The effect of each light is computed per-pixel, so there are no lighting computations that break down on large triangles.

On the downside, deferred shading has no real support for anti-aliasing and can't handle semi-transparent GameObjects (these are rendered using [forward](RenderTech-ForwardRendering) rendering). There is also no support for the Mesh Renderer's Receive Shadows flag and culling masks are only supported in a limited way. You can only use up to four culling masks. That is, your culling layer mask must at least contain all layers minus four arbitrary layers, so 28 of the 32 layers must be set. Otherwise you get graphical artefacts.

## Requirements


It requires a graphics card with Multiple Render Targets (MRT), Shader Model 3.0 (or later) and support for Depth render textures. Most PC graphics cards made after 2006 support deferred shading, starting with GeForce 8xxx, Radeon X2400, Intel G45.

On mobile, deferred shading is not supported, mostly due to MRT formats used (some GPUs which do support multiple render targets, still only support very limited bit counts).

**Note:** Deferred rendering is not supported when using Orthographic projection. If the Camera's projection mode is set to Orthographic, the Camera falls back to Forward rendering.

## Performance considerations


The rendering overhead of realtime lights in deferred shading is proportional to the number of pixels illuminated by the light and _not_ dependent on Scene complexity. So small point or spot lights are very cheap to render and if they are fully or partially occluded by Scene GameObjects then they are even cheaper.

Of course, lights with shadows are much more expensive than lights without shadows. In deferred shading, shadow-casting GameObjects still need to be rendered once or more for each shadow-casting light. Furthermore, the lighting shader that applies shadows has a higher rendering overhead than the one used when shadows are disabled.


## Implementation details


When deferred shading is used, the rendering process in Unity happens in two passes:


1. G-buffer Pass: GameObjects are rendered to produce screen-space buffers with diffuse color, specular color, smoothness,
world space normal, emission and depth.
1. Lighting pass: the previously generated buffers are used to add lighting into emission buffer.

Objects with shaders that can't handle deferred shading are rendered after this process is complete, using the [forward rendering](RenderTech-ForwardRendering) path.

The default g-buffer layout is as follows:

* RT0, ARGB32 format: Diffuse color (RGB), occlusion (A).
* RT1, ARGB32 format: Specular color (RGB), roughness (A).
* RT2, ARGB2101010 format: World space normal (RGB), unused (A).
* RT3, ARGB2101010 (non-HDR) or ARGBHalf (HDR) format: Emission + lighting + lightmaps + reflection probes buffer.
* Depth+Stencil buffer.

So the default g-buffer layout is 160 bits/pixel (non-HDR) or 192 bits/pixel (HDR).

Emission+lighting buffer (RT3) is logarithmically encoded to provide greater dynamic range than is usually possible with an ARGB32 texture, when the Camera is not using HDR.

Note that when the Camera is using HDR rendering, then there's no separate render target being created for Emission+lighting buffer (RT3); instead the render target that the Camera renders into (that is, the one that is passed to the image effects) is used as RT3.


### G-Buffer pass

The g-buffer pass renders each GameObject once. Diffuse and specular colors, surface smoothness, world space normal, and emission+ambient+reflections+lightmaps are rendered into g-buffer textures. The g-buffer textures are setup as global shader properties for later access by shaders (_CameraGBufferTexture0 .. _CameraGBufferTexture3 names).


### Lighting pass

The lighting pass computes lighting based on g-buffer and depth. Lighting is computed in screen space, so the time it takes to process is independent of Scene complexity. Lighting is added to the emission buffer.

Point and spot lights that do not cross the Camera's near plane are rendered as 3D shapes, with the Z buffer's test against the Scene enabled. This makes partially or fully occluded point and spot lights very cheap to render. Directional lights and point/spot lights that cross the near plane are rendered as fullscreen quads.

If a light has shadows enabled then they are also rendered and applied in this pass. Note that shadows do not come for "free"; shadow casters need to be rendered and a more complex light shader must be applied.

The only lighting model available is Standard. If a different model is wanted you can modify the lighting pass shader, by placing the modified version of the Internal-DeferredShading.shader file from the [Built-in shaders](http://unity3d.com/support/resources/assets/built-in-shaders) into a folder named "Resources" in your "Assets" folder.  Then go to the Edit->Project Settings->Graphics window.  Changed the "Deferred" dropdown to "Custom Shader".  Then change the Shader option which appears to the shader you are using.

