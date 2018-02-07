# Lightmaps: Technical information

Unity stores lightmaps with different compressions and encoding schemes, depending on the target platform and the compression setting in the Lighting Window.

##Encoding schemes

Unity projects can use two techniques to encode baked light intensity ranges into low dynamic range textures when this is needed:

* **RGBM encoding**. RGBM encoding stores a color in the **RGB** channels and a multiplier (**M**) in the alpha channel. The range of RGBM lightmaps goes from 0 to 34.49(5<sup>2.2</sup>) in linear space, and from 0 to 5 in gamma space.

* **Double Low Dynamic Range (dLDR) encoding**. dLDR encoding is used on mobile platforms by simply mapping a range of [0, 2] to [0, 1]. Baked light intensities that are above a value of 2 will be clamped. The decoding value is computed by multiplying the value from the lightmap texture by 2 when gamma space is used, or 4.59482(2<sup>2.2</sup>) when linear space is used. Some platforms store lightmaps as dLDR because their hardware compression produces poor-looking artifacts when using RGBM.

When Linear Color Space is used, the lightmap texture is marked as sRGB and the final value used by the shaders (after sampling and decoding) will be in Linear Color Space. When Gamma Color Space is used, the final value will be in Gamma Color Space.

**Note**: When encoding is used, the values stored in the lightmaps (GPU texture memory) are always in Gamma Color Space. 

The __Decode Lightmap__ shader function from the _UnityCG.cginc_ shader include file handles the decoding of lightmap values after the value is read from the lightmap texture in a shader.

##HDR lightmap support

HDR lightmaps can be used on PC, Mac & Linux Standalone, Xbox One, and PlayStation 4. The Player Settings inspector has a **Lightmap Encoding** option for these platforms, which controls the encoding/compression of the lightmaps.

![](../uploads/Main/LightmapsTechnicalDetails.png)

Choosing __High Quality__ will enable HDR lightmap support, whereas __Normal Quality__ will switch to using __RGBM__ encoding.

When lightmap __Compression__ is enabled in the Lighting Window, the lightmaps will be compressed using the __BC6H__ compression format.

##Advantages of High Quality (BC6H) lightmaps

* HDR lightmaps don’t use any encoding scheme to encode lightmap values, so the supported range is only limited by the 16-bit floating point texture format that goes from 0 to 65504. 

* BC6H format quality is superior to DXT5 + RGBM format encoding, and it doesn’t produce any of the color banding artifacts that RGBM encoding has. 

* Shaders that need to sample HDR lightmaps are a few ALU instructions shorter because there is no need to decode the sampled values. 

* BC6H format has the same GPU memory requirements as DXT5.

Here is the list of encoding schemes and their texture compression formats per target platform:

| **Target platform** | **Encoding** | **Compression - size (bits per pixel)** |
|:--|:--|:--|
| Standalone(PC, Mac, Linux) | RGBM / HDR | DXT5 / BC6H - 8 bpp |
| Xbox One | RGBM / HDR | DXT5 / BC6H - 8 bpp |
| PlayStation4 | RGBM / HDR | DXT5 / BC6H - 8 bpp |
| WebGL 1.0 / 2.0 | RGBM | DXT5 - 8 bpp |
| iOS | dLDR | PVRTC RGB - 4 bpp |
| tvOS | dLDR | ASTC 4x4 block RGB - 8 bpp |
| Android* | dLDR | ETC1 RGB - 4 bpp |
| Samsung TV | dLDR | ETC1 RGB - 4 bpp |
| Nintendo 3DS | dLDR | ETC1 RGB - 4 bpp |
| Nintendo 3DS | dLDR | ETC1 RGB - 4 bpp |

*If the target is __Android__ then you can override the default texture compression format from the __Build Settings__ to one of the following formats: DXT1, PVRTC, ATC, ETC2, ASTC. The default format is ETC.

##Precomputed real-time Global Illumination (GI)

The inputs to the GI system have a different range and encoding to the output. Surface albedo is 8-bit unsigned integer RGB in gamma space and emission is 16-bit floating point RGB in linear space. For advice on providing custom inputs using a meta pass, see documentation on [Meta pass](MetaPass).

The irradiance output texture is stored using the RGB9E5 shared exponent floating point format if the graphics hardware supports it, or RGBM with a range of 5 as fallback. The range of RGB9E5 lightmaps is [0, 65408]. For details on the RGB9E5 format, see [Khronos.org: EXT_texture_shared_exponent](https://www.khronos.org/registry/OpenGL/extensions/EXT/EXT_texture_shared_exponent.txt).

See also:

* [Texture Importer Override](class-TextureImporterOverride)
* [Texture Types](TextureTypes) 
* [Global Illumination](GlobalIllumination)
* [Texture Types](TextureTypes) 
* [Global Illumination](GlobalIllumination)

---

* <span class="page-edit">2017-09-18  <!-- include IncludeTextAmendPageNoEdit --></span>

* <span class="page-history">Baked lightmaps added in Unity [2017.2](https://docs.unity3d.com/2017.2/Documentation/Manual/30_search.html?q=newin20172) <span class="search-words">NewIn20172</span></span>

* <span class="page-history">HDR lightmap support added in Unity [2017.3](https://docs.unity3d.com/2017.3/Documentation/Manual/30_search.html?q=newin20173) <span class="search-words">NewIn20173</span></span>