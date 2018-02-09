#Texture compression formats for platform-specific overrides

While Unity supports many common image formats as source files for importing your [Textures](class-TextureImporter) (such as JPG, PNG, PSD and TGA), these formats are not used during realtime rendering by 3D graphics hardware such as a graphics card or mobile device. 3D graphics hardware requires Textures to be compressed in specialized formats which are optimised for fast Texture sampling. The various different platforms and devices available each have their own different proprietary formats.

By default, the Unity Editor automatically converts Textures to the most appropriate format to match the build target you have selected. Only the  converted Textures are included in your build; your source Asset files are left in their original format, in your project’s _Assets_ folder. However, on most platforms there are a number of different supported Texture compression formats to choose from. Unity has certain default formats set up for each platform, but in some situations you may want to override the default and pick a different compression format for some of your Textures (for example, if you are using a Texture as a mask, with only one channel, you might choose to use the BC4 format to save space while preserving quality).

To apply custom settings for each platform, use the [Texture Importer](class-TextureImporter) to set default options, then use the __Platform-specific overrides__ panel to override those defaults for specific platforms.

![Default internal Texture representation per platform
](../uploads/Main/class-TextureImporterOverride.png)

The following table shows the default formats used for each platform. 

| **Platform** | **Color model** | **None** | **Normal quality (Default)** | **High quality** | **Low quality (higher performance)** |
|:---|:---|:---|:---|:---|:---| 
| Windows, Linux, macOS, PS4, XBox One| RGB | RGB 24 bit | RGB Compressed DXT1 | RGB(A) Compressed BC7 | RGB Compressed DXT1 |
| | RGBA | RGBA 32 bit | RGBA Compressed DXT5 | RGB(A) Compressed BC7 | RGBA Compressed DXT5 |
| | HDR | RGBA Half | RGB Compressed BC6H  | RGB Compressed BC6H  | RGB Compressed BC6H  |
| WebGL| RGB | RGB 24 bit | RGB Compressed DXT1 | RGB Compressed DXT1 | RGB Compressed DXT1 |
| | RGBA | RGBA 32 bit | RGBA Compressed DXT5 | RGBA Compressed DXT5 | RGBA Compressed DXT5 |
| Android (default subTarget)| RGB | RGB 24 bit | RGB Compressed ETC2 | RGB Compressed ETC2 | RGB Compressed ETC2 |
| | RGBA | RGBA 32 bit | RGBA Compressed ETC2 | RGBA Compressed ETC2 | RGBA Compressed ETC2 |
| iOS| RGB | RGB 24 bit | RGB Compressed PVRTC 4 bits | RGB Compressed PVRTC 4 bits | RGB Compressed PVRTC 2 bits |
| | RGBA | RGBA 32 bit | RGBA Compressed PVRTC 4 bits | RGBA Compressed PVRTC 4 bits | RGBA Compressed PVRTC 2 bits |
| tvOS| RGB | RGB 24 bit | RGB Compressed ASTC 6x6 block | RGB Compressed ASTC 4x4 block | RGB Compressed ASTC 8x8 block |
| | RGBA | RGBA 32 bit | RGBA Compressed ASTC 6x6 block | RGBA Compressed ASTC 4x4 block | RGBA Compressed ASTC 8x8 block |
| Tizen, Samsung TV| RGB | RGB 24 bit  | RGB Compressed ETC | RGB Compressed ETC | RGB Compressed ETC |
| | RGBA | RGBA 32 bit | RGBA 16 bit | RGBA 16 bit | RGBA 16 bit |



### All supported Texture compression formats

The following table shows the Texture compression format options available on each platform, and the resulting compressed file size (based on a 256px-square image). Choosing a Texture compression format is a balance between file size and quality; the higher the quality, the greater the file size. In the description below, see the final file size of a in-game Texture of 256 by 256 pixels.

When you use a Texture compression format that is not supported on the target platform, the Textures are decompressed to RGBA 32 and stored in memory alongside the compressed Textures. When this happens, time is lost decompressing Textures, and memory is lost because you are storing them twice. In addition, all platforms have different hardware, and are optimised to work most efficiently with specific compression formats; choosing non-compatible formats can impact your game's performance. The table below shows supported platforms for each compression format.

Notes on the table below:

* __RGB__ is a color model in which red, green and blue are added together in various ways to reproduce a broad array of [colors](https://en.wikipedia.org/wiki/Color). 

* __RGBA__ is a version of __RGB__ with an alpha channel, which supports blending and opacity alteration.

* __Crunch compression __is a lossy compression format (meaning that parts of the [data](https://simple.wikipedia.org/wiki/Information) are lost during compression) on top of DXT Texture compression. Textures are decompressed to DXT on the CPU, and then uploaded to the GPU at runtime. Crunch compression helps the Texture use the lowest possible amount of space on disk and for downloads. Crunch Textures can take a long time to compress, but decompression at runtime is very fast.

| **Texture compression format**| **Description** | **Size** <br/>for a 256x256 pixel Texture | **Platform Support** |
|:---|:---|:---|:---| 
| RGB Compressed DXT1 | Compressed unsigned normalised integer RGB Texture. | 32KB (4 bits per pixel) | Windows, Linux, macOS, PS4, XBox One, Android (Nvidia Tegra and Intel Bay Trail), WebGL |
| RGBA Compressed DXT5| Compressed unsigned normalised integer RGBA Texture. 8 bits per pixel. | 64KB (8 bits per pixel) | Windows, Linux, macOS, PS4, XBox One, Android (Nvidia Tegra and Intel Bay Trail), WebGL |
| RGB Crunched DXT1| Similar to RGB Compressed DXT1, but compressed using crunch compression. See Notes, above, for more on crunch compression. | Variable, depending on the complexity of the content in the texture. | Windows, Linux, macOS, PS4, XBox One, Android (Nvidia Tegra and Intel Bay Trail), WebGL |
| RGBA Crunched DXT5  | Similar to RGBA Crunched DXT5, but compressed using crunch compression. See Notes, above, for more on crunch compression. | Variable, depending on the complexity of the content in the texture. | Windows, Linux, macOS, PS4, XBox One, Android (Nvidia Tegra and Intel Bay Trail), WebGL |
| RGB Compressed BC6H | Compressed unsigned float/High Dynamic Range (HDR) RGB Texture.  | 64KB (8 bits per pixel) | Windows Direct3D 11: OpenGL 4, Linux. <br/>Note: BC6H Textures are uncompressed at runtime to RGBA half on the following platform configurations: <br/>Windows with Direct3D 9<br/>macOS with OpenGL<br/>Platforms with Direct3D 10 Shader Model 4 or OpenGL 3 GPUs  |
| RGB(A) Compressed BC7| High-quality compressed unsigned normalised integer RGB or RGBA Texture.  | 64KB (8 bits per pixel) | Windows Direct3D 11: OpenGL 4, Linux <br/>Note: BC7 Textures are uncompressed at runtime to RGBA 32bits on the following platform configurations: <br/>Windows with Direct3D 9<br/>macOS with OpenGL<br/>Platforms with Direct3D 10 Shader Model 4<br/>Platforms with OpenGL 3 GPUs. |
| RGB Compressed ETC| Compressed RGB Texture.<br/>Note: ETC1 is supported by all OpenGL ES 2.0 GPUs. It does not support alpha. | 32KB (4 bits per pixel) | Android, Tizen, Samsung TV |
| RGB Compressed ETC2| Compressed RGB Texture. This is the default Texture compression format for Android projects.<br/>Note: ETC2 is part of OpenGL ES 3.0. It does not support alpha. On Android platforms that don’t support ETC2, the Texture is uncompressed at runtime to RGB 24 bit. | 32KB (4 bits per pixel) | Android (OpenGL ES 3.0) <br/>Note: On Android mobiles that don’t support ETC2, the Texture is uncompressed at runtime to RGBA32 |
| RGBA Compressed ETC2 | Compressed RGBA Texture. 8 bits per pixel (64KB for a 256x256 Texture). This is the default Texture compression format for Android projects. <br/>Note: ETC2 is part of OpenGL ES 3.0. It does not support alpha. On Android platforms that don’t support ETC2, the Texture are uncompressed at runtime to RGBA 32 bit. | 64KB (8 bits per pixel) | Android (OpenGL ES 3.0) <br/>Note: On Android mobiles that don’t support ETC2, the Texture is uncompressed at runtime to RGBA32 |
| RGB Compressed ASTC| Variable block size compressed RGB Texture. | 12x12: 0.89 bits per pixel (7.56KB for a 256x256 Texture)<br/>10x10: 1.28 bits per pixel (10.56KB for a 256x256 Textures)<br/>8x8: 2 bits per pixel (16KB for a 256x256 Texture); <br/>6x6: 3.56 bits per pixel (28.89KB for a 256x256 Texture)<br/>5x5: 5.12 bits per pixel (42.25KB for a 256x256 Texture)<br/>4x4: 8 bits per pixel (64KB for a 256x256 Texture) | tvOS (all), iOS (A8), Android (PowerVR 6XT, Mali T600 series, Adreno 400 series, Tegra K1) |
| RGBA Compressed ASTC| Variable block size compressed RGBA Texture. | 12x12: 0.89 bits per pixel (7744 bytes for a 256x256 Texture)<br/>10x10: 1.28 bits per pixel (10816 bytes for a 256x256 Textures)<br/>8x8: 2 bits per pixel (16KB for a 256x256 Texture); <br/>6x6: 3.56 bits per pixel (29584 bytes for a 256x256 Texture)<br/>5x5: 5.12 bits per pixel (43264 bytes for a 256x256 Texture)<br/>4x4: 8 bits per pixel (64KB for a 256x256 Texture) | tvOS (all), iOS (A8), Android (PowerVR 6XT, Mali T600 series, Adreno 400 series, Tegra K1) |
| RGB Compressed PVRTC 2 bits| High-compression RGB Texture. Low quality, but lower size, resulting in higher performance. | 16KB (2 bits per pixel) | Android (PowerVR), iOS, tvOS |
| RGBA Compressed PVRTC 2 bits| High-compression RGBA Texture. Low quality, but lower size, resulting in higher performance. | 16KB (2 bits per pixel) | Android (PowerVR), iOS, tvOS |
| RGB Compressed PVRTC 4 bits| Compressed RGB Texture. High-quality Textures, particularly on color data, but can take a long time to compress. | 32KB (4 bits per pixel) | Android (PowerVR), iOS, tvOS |
| RGBA Compressed PVRTC 4 bits| Compressed RGB Texture. High-quality Textures, particularly on color data, but can take a long time to compress. | 32KB (4 bits per pixel) | Android (PowerVR), iOS, tvOS |
| RGB Compressed ATC| Compressed RGB Texture. | 32KB (4 bits per pixel) | Android (Qualcomm - Adreno), iOS, tvOS |
| RGBA Compressed ATC| Compressed RGBA Texture. | 64KB (8 bits per pixel) | Android (Qualcomm - Adreno), iOS, tvOS |
| RGB 16 bit| 65 thousand colors with no alpha. Uses more memory than the compressed formats, but could be more suitable for UI or crisp Textures without gradients. | 128KB (16 bits per pixel) | All platforms |
| RGB 24 bit| True color, but without alpha.  | 192KB (24 bits per pixel) | All platforms |
| Alpha 8| High-quality alpha channel, but without any color.  | 64KB (8 bits per pixel) | All platforms |
| RGBA 16 bit| Low-quality true color. This is the default compression for Textures that have an alpha channel.  | 128KB (16 bits per pixel) | All platforms |
| RGBA 32 bit| True color with alpha. This is the highest quality compression for Textures that have an alpha channel. | 256KB (32 bits per pixel) | All platforms |

You can import Textures from DDS files, but only DXT, BC compressed formats, or uncompressed pixel formats are supported.

### Notes on Android

Unless you’re targeting specific hardware (such as Tegra), ETC2 compression is the most efficient option for Android, offering the best balance of quality and file size (with associated memory size requirements). If you need an alpha channel, you could store it externally and still benefit from a lower Texture file size.

You can use ETC1 for Textures that have an [alpha channel](HOWTO-alphamaps.html), but only if the build is for Android and the Textures are placed on an atlas (by specifying the packing tag). To enable this, tick the __Compress using ETC1__ checkbox for the Texture. Unity splits the resulting atlas into two Textures, each without an alpha channel, and then combines them in the final parts of the render pipeline.

To store an alpha channel in a Texture, use RGBA16 bit compression, which is supported by all hardware vendors.