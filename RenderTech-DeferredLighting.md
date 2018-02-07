# Legacy Deferred Lighting Rendering Path


This page details the *Legacy Deferred Lighting (light prepass)* [rendering path](RenderingPaths). See [this article](http://www.realtimerendering.com/blog/deferred-lighting-approaches/) for a technical overview of deferred lighting.

**Note**: Deferred Lighting is considered a legacy feature starting with Unity 5.0, as it does not support some of the rendering features (e.g. Standard shader, reflection probes). New projects should consider using [Deferred Shading](RenderTech-DeferredShading) rendering path instead.

**NOTE:** *Deferred rendering is not supported when using Orthographic projection. If the camera's projection mode is set to Orthographic, the camera will always use Forward rendering.*

## Overview

When using Deferred Lighting, there is no limit on the number of lights that can affect an object. All lights are evaluated per-pixel, which means that they all interact correctly with normal maps, etc. Additionally, all lights can have cookies and shadows.

Deferred lighting has the advantage that the processing overhead of lighting is proportional to the number of pixels the light shines on. This is determined by the size of the light volume in the scene regardless of how many objects it illuminates. Therefore, performance can be improved by keeping lights small. Deferred lighting also has highly consistent and predictable behaviour. The effect of each light is computed per-pixel, so there are no lighting computations that break down on large triangles.

On the downside, deferred lighting has no real support for anti-aliasing and can't handle semi-transparent objects (these will be rendered using [forward](RenderTech-ForwardRendering) rendering). There is also no support for the Mesh Renderer's Receive Shadows flag and culling masks are only supported in a limited way. You can only use up to four culling masks. That is, your culling layer mask must at least contain all layers minus four arbitrary layers, so 28 of the 32 layers must be set. Otherwise you will get graphical artefacts.


## Requirements

It requires a graphics card with Shader Model 3.0 (or later), support for Depth render textures and two-sided stencil buffers.
Most PC graphics cards made after 2004 support deferred lighting, including GeForce FX and later, Radeon X1300 and later,
Intel 965 / GMA X3100 and later. On mobile, all OpenGL ES 3.0 capable GPUs support deferred lighting, and some of
OpenGL ES 2.0 capable ones support it too (the ones that do support depth textures).


## Performance Considerations


The rendering overhead of realtime lights in deferred lighting is proportional to the number of pixels illuminated by the light and is _not_ dependent on scene complexity. So small point or spot lights are very cheap to render and if they are fully or partially occluded by scene objects then they are even cheaper.

Of course, lights with shadows are much more expensive than lights without shadows. In deferred lighting, shadow-casting objects still need to be rendered once or more for each shadow-casting light. Furthermore, the lighting shader that applies shadows has a higher rendering overhead than the one used when shadows are disabled.

## Implementation Details


When Deferred Lighting is used, the rendering process in Unity happens in three passes:


1. Base Pass: objects are rendered to produce screen-space buffers with depth, normals, and specular power.
1. Lighting pass: the previously generated buffers are used to compute lighting into another screen-space buffer.
1. Final pass: objects are rendered again. They fetch the computed lighting, combine it with color textures and add any ambient/emissive lighting.

Objects with shaders that can't handle deferred lighting are rendered after this process is complete, using the [forward rendering](RenderTech-ForwardRendering) path.


###Base Pass

The base pass renders each object once. View space normals and specular power are rendered into a single ARGB32 [Render Texture](class-RenderTexture) (with normals in RGB channels and specular power in A). If the platform and hardware allow the Z buffer to be read as a texture then depth is not explicitly rendered. If the Z buffer can't be accessed as a texture then depth is rendered in an additional rendering pass using [shader replacement](SL-ShaderReplacement).

The result of the base pass is a Z buffer filled with the scene contents and a Render Texture with normals and specular power.


###Lighting Pass

The lighting pass computes lighting based on depth, normals and specular power. Lighting is computed in screen space, so the time it takes to process is independent of scene complexity. The lighting buffer is a single ARGB32 Render Texture, with diffuse lighting in the RGB channels and monochrome specular lighting in the A channel. Lighting values are logarithmically encoded to provide greater dynamic range than is usually possible with an ARGB32 texture. When a camera has HDR rendering enabled, then lighting buffer is of ARGBHalf format, and logarithmic encoding is not performed.

Point and spot lights that do not cross the camera's near plane are rendered as (front faces of) 3D shapes, with the depth test against the scene enabled. Lights crossing the near plane are also rendered using 3D shapes, but as back faces with inverted depth test instead. This makes partially or fully occluded lights very cheap to render. If a light intersects both far and near camera planes at the same time, the above optimizations cannot be used, and the light is drawn as a tight quad with no depth testing.

The above doesn't apply to directional lights, which are always rendered as fullscreen quads.

If a light has shadows enabled then they are also rendered and applied in this pass. Note that shadows do not come for "free"; shadow casters need to be rendered and a more complex light shader must be applied.

The only lighting model available is Blinn-Phong. If a different model is wanted you can modify the lighting pass shader, by placing the modified version of the Internal-PrePassLighting.shader file from the [Built-in shaders](http://unity3d.com/support/resources/assets/built-in-shaders) into a folder named "Resources" in your "Assets" folder. Then go to the Edit->Project Settings->Graphics window.  Changed the "Legacy Deferred" dropdown to "Custom Shader".  Then change the Shader option which appears to the lighting shader you are using.

###Final Pass

The final pass produces the final rendered image. Here all objects are rendered again with shaders that fetch the lighting, combine it with textures and add any emissive lighting. Lightmaps are also applied in the final pass. Close to the camera, realtime lighting is used, and only baked indirect lighting is added. This crossfades into fully baked lighting further away from the camera.
