#iOS 2D Texture Overrides

When you are building for different platforms, you have to think about the resolution of your textures for the target platform, the size and the quality. You can set default options and then override the defaults for a specific platform.

This page details the __Texture Overrides__ specific to iOS. A description of the general Texture Overrides can be found [here](class-TextureImporter).

![](../uploads/Main/TextureImporterOverride.png) 

| | |
|:---|:---|
|__Texture Format__ |What internal representation is used for the texture. This is a tradeoff between size and quality. In the examples below we show the final size of a in-game texture of 256 by 256 pixels:|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGB Compressed PVRTC 4 bits__ |Compressed RGB texture. This is the most common format for diffuse textures. 4 bits per pixel (32 KB for a 256x256 texture) |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGBA Compressed PVRTC 4 bits__ |Compressed RGBA texture. This is the main format used for diffuse & specular control textures or diffuse textures with transparency. 4 bits per pixel (32 KB for a 256x256 texture) |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGB Compressed PVRTC 2 bits__ |Compressed RGB texture. Lower quality format suitable for diffuse textures. 2 bits per pixel (16 KB for a 256x256 texture) |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGBA Compressed PVRTC 2 bits__ |Compressed RGBA texture. Lower quality format suitable for diffuse & specular control textures. 2 bits per pixel (16 KB for a 256x256 texture) |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGB Compressed DXT1__ |Compressed RGB texture. This format is not supported on iOS, but kept for backwards compatibility with desktop projects. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGBA Compressed DXT5__ |Compressed RGBA texture. This format is not supported on iOS, but kept for backwards compatibility with desktop projects. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGB 16 bit__ |65 thousand colors with no alpha. Uses more memory than PVRTC formats, but could be more suitable for UI or crisp textures without gradients. 128 KB for a 256x256 texture. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGB 24 bit__ |Truecolor but without alpha. 192 KB for a 256x256 texture. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Alpha 8 bit__ |High quality alpha channel but without any color. 64 KB for a 256x256 texture. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGBA 16 bit__ |Low-quality truecolor. Has 16 levels of red, green, blue and alpha. Uses more memory than PVRTC formats, but can be handy if you need exact alpha channel. 128 KB for a 256x256 texture. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGBA 32 bit__ |Truecolor with alpha - this is the highest quality. At 256 KB for a 256x256 texture, this one is expensive. Most of the time, **PVRTC** formats offers sufficient quality at a much smaller size. |
|__Compression quality__ | Choose Fast for quickest performance, Best for the best image quality and Normal for a balance between the two. |

