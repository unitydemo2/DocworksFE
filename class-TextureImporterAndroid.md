#Android 2D Textures Overrides

When you are building for different platforms, you have to think about the resolution of your textures for the target platform, the size and the quality. You can set default options and then override the defaults for a specific platform.

This page details the __Texture Overrides__ specific to Android. A description of the general Texture Overrides can be found [here](class-TextureImporter).

![](../uploads/Main/TextureImporterOverride.png) 


| | |
|:---|:---|
|__Texture Format__ |What internal representation is used for the texture. This is a tradeoff between size and quality. In the examples below we show the final size of a in-game texture of 256 by 256 pixels:|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGB Compressed DXT1__ |Compressed RGB texture. Supported by Nvidia Tegra. 4 bits per pixel (32 KB for a 256x256 texture). |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGBA Compressed DXT5__ |Compressed RGBA texture. Supported by Nvidia Tegra. 6 bits per pixel (64 KB for a 256x256 texture). |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGB Compressed ETC 4 bits__ |Compressed RGB texture. This is the default texture format for Android projects. ETC1 is part of OpenGL ES 2.0 and is supported by all OpenGL ES 2.0 GPUs. It does not support alpha. 4 bits per pixel (32 KB for a 256x256 texture) |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGB Compressed PVRTC 2 bits__ |Compressed RGB texture. Supported by Imagination PowerVR GPUs. 2 bits per pixel (16 KB for a 256x256 texture) |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGBA Compressed PVRTC 2 bits__ |Compressed RGBA texture. Supported by Imagination PowerVR GPUs. 2 bits per pixel (16 KB for a 256x256 texture) |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGB Compressed PVRTC 4 bits__ |Compressed RGB texture. Supported by Imagination PowerVR GPUs. 4 bits per pixel (32 KB for a 256x256 texture) |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGBA Compressed PVRTC 4 bits__ |Compressed RGBA texture. Supported by Imagination PowerVR GPUs. 4 bits per pixel (32 KB for a 256x256 texture) |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGB Compressed ATC 4 bits__ |Compressed RGB texture. Supported by Qualcomm Snapdragon. 4 bits per pixel (32 KB for a 256x256 texture). |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGBA Compressed ATC 8 bits__ |Compressed RGBA texture. Supported by Qualcomm Snapdragon. 6 bits per pixel (64 KB for a 256x256 texture). |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGB 16 bit__ |65 thousand colors with no alpha. Uses more memory than the compressed formats, but could be more suitable for UI or crisp textures without gradients. 128 KB for a 256x256 texture. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGB 24 bit__ |Truecolor but without alpha. 192 KB for a 256x256 texture. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Alpha 8 bit__ |High quality alpha channel but without any color. 64 KB for a 256x256 texture. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGBA 16 bit__ |Low-quality truecolor. The default compression for the textures with alpha channel. 128 KB for a 256x256 texture. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__RGBA 32 bit__ |Truecolor with alpha - this is the highest quality compression for the textures with alpha. 256 KB for a 256x256 texture. |
|__Compression quality__ | Choose Fast for quickest performance, Best for the best image quality and Normal for a balance between the two. |

Unless you're targeting a specific hardware, like Tegra, we'd recommend using ETC1 compression. If needed you could store an external alpha channel and still benefit from lower texture footprint.

Unity can use ETC1 for textures with Alpha, provided they are placed on some Atlas (by specifying the packing tag) and the build is for Android. You can opt in for this by setting the "Compress using ETC1" checkbox for the texture. Under the hood Unity will split the resulting atlas into two textures, each without alpha and then combine them in the final parts of the render-pipeline.

If you absolutely want to store an alpha channel in a texture, RGBA16 bit is the compression supported by all hardware vendors.


Textures can be imported from DDS files but only DXT or uncompressed pixel formats are currently supported. 

If your app utilizes an unsupported texture compression, the textures will be uncompressed to RGBA 32 and stored in memory along with the compressed ones.
So in this case you lose time decompressing textures and lose memory storing them twice. It may also have a very negative impact on rendering performance.

