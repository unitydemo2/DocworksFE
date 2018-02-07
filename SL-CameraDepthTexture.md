# Camera's Depth Texture


A [Camera](class-Camera) can generate a depth, depth+normals, or motion vector Texture. This is a minimalistic G-buffer Texture that can be used for post-processing effects or to implement custom lighting models (e.g. light pre-pass). It is also possible to build similar textures yourself, using [Shader Replacement](SL-ShaderReplacement) feature.

The Camera's depth Texture mode can be enabled using [Camera.depthTextureMode](ScriptRef:Camera-depthTextureMode.html) variable from script.

There are three possible depth texture modes:

* __DepthTextureMode.Depth__: a [depth texture](SL-DepthTextures).
* __DepthTextureMode.DepthNormals__: depth and view space normals packed into one texture.* 
* __DepthTextureMode.MotionVectors__: per-pixel screen space motion of each screen texel for the current frame. Packed into a RG16 texture.

These are flags, so it is possible to specify any combination of the above textures.

## DepthTextureMode.Depth texture


This builds a screen-sized [depth texture](SL-DepthTextures).

Depth texture is rendered using the same shader passes as used for shadow caster rendering (`ShadowCaster` pass type). So by extension, if a shader does not support shadow casting (i.e. there's no shadow caster pass in the shader or any of the fallbacks), then objects using that shader will not show up in the depth texture.

* Make your shader [fallback](SL-Fallback) to some other shader that has a shadow casting pass, or
* If you're using [surface shaders](SL-SurfaceShaders), adding an `addshadow` directive will make them generate a shadow pass too.

Note that only "opaque" objects (that which have their materials and shaders setup to use [render queue](SL-SubShaderTags) <= 2500) are rendered into the depth texture.


## DepthTextureMode.DepthNormals texture


This builds a screen-sized 32 bit (8 bit/channel) texture, where view space normals are encoded into R&G channels, and depth is encoded in B&A channels. Normals are encoded using Stereographic projection, and depth is 16 bit value packed into two 8 bit channels.

[`UnityCG.cginc` include file](SL-BuiltinIncludes) has a helper function `DecodeDepthNormal` to decode depth and normal from the encoded pixel value. Returned depth is in 0..1 range.

For examples on how to use the depth and normals texture, please refer to the EdgeDetection image effect in the Shader Replacement example project or [Screen Space Ambient Occlusion Image Effect](PostProcessing-AmbientOcclusion).

## DepthTextureMode.MotionVectors texture


This builds a screen-sized RG16 (16-bit float/channel) texture, where screen space pixel motion is encoded into the R&G channels. The pixel motion is encoded in screen UV space.

When sampling from this texture motion from the encoded pixel is returned in a rance of -1..1. This will be the UV offset from the last frame to the current frame. 


## Tips & Tricks

[Camera inspector](class-Camera) indicates when a camera is rendering a depth or a depth+normals texture.

The way that depth textures are requested from the Camera ([Camera.depthTextureMode](ScriptRef:Camera-depthTextureMode.html)) might mean that after you disable an effect that needed them, the Camera might still continue rendering them. If there are multiple effects present on a Camera, where each of them needs the depth texture, there's no good way to automatically disable depth texture rendering if you disable the individual effects.

When implementing complex Shaders or Image Effects, keep [Rendering Differences Between Platforms](SL-PlatformDifferences) in mind. In particular, using depth texture in an Image Effect often needs special handling on Direct3D + Anti-Aliasing.

In some cases, the depth texture might come directly from the native Z buffer. If you see artifacts in your depth texture, make sure that the shaders that use it **do not** write into the Z buffer (use [ZWrite Off](SL-CullAndDepth)).


## Shader variables

Depth textures are available for sampling in shaders as global shader properties. By declaring a sampler called `_CameraDepthTexture` you will be able to sample the main depth texture for the camera.

`_CameraDepthTexture` always refers to the camera's primary depth 
texture. By contrast, you can use `_LastCameraDepthTexture` to refer to the last depth texture rendered by any camera. This could be useful for example if you render a half-resolution depth texture in script using a secondary camera and want to make it available to a post-process shader.

The motion vectors texture (when enabled) is available in Shaders as a global Shader property. By declaring a sampler called '_CameraMotionVectorsTexture' you can sample the Texture for the curently rendering Camera. 

## Under the hood

Depth textures can come directly from the actual depth buffer,
or be rendered in a separate pass, depending on the rendering
path used and the hardware. Typically when using Deferred
Shading or Legacy Deferred Lighting rendering paths, the depth textures come "for free" since they are a product of the
G-buffer rendering anyway.

When the DepthNormals texture is rendered in a separate pass, this is done through [Shader Replacement](SL-ShaderReplacement). Hence it is important to have correct "__RenderType__" tag in your shaders.

When enabled, the MotionVectors texture always comes from a extra render pass. Unity will render moving GameObjects into this buffer, and construct their motion from the last frame to the current frame. 


## See also

* [Writing Image Effects](PostProcessingWritingEffects)
* [Depth Textures](SL-DepthTextures)
* [Shader Replacement](SL-ShaderReplacement)


