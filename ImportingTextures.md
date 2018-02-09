# Importing Textures

This page offers details and tips on importing [Textures](Textures) using the Unity Editor [Texture Importer](class-TextureImporter). Scroll down or select an area you wish to learn about.

* [Supported file formats](#Formats)
* [HDR Textures](#HDRTextures)
* [Texture sizes](#TextureSizes)
* [UV mapping](#UVmapping)
* [Mip maps](#Mipmaps)
* [Normal maps](#Normalmaps)
* [Detail maps](#Detailmaps)
* [Reflections (cubemaps)](#Reflections)
* [Anisotropic filtering](#AnisotropicFiltering)

<a name="Formats"></a>
## Supported file formats

Unity can read the following file formats: 

* BMP
* EXR
* GIF
* HDR
* IFF
* JPG
* PICT
* PNG
* PSD 
* TGA
* TIFF 

Note that Unity can import multi-layer PSD and TIFF files; they are flattened automatically on import, but the layers are maintained in the Assets themselves. This means that you don’t lose any of your work when using these file types natively. This is important, because it allows you to have just one copy of your Textures which you can use in different applications; Photoshop, your 3D modelling app, and in Unity.

<a name="HDRTextures"></a>
## HDR Textures

When importing from an EXR or HDR file containing HDR information, the [Texture Importer](class-TextureImporter) automatically chooses the right HDR format for the output Texture. This format changes automatically depending on which platform you are building for.

<a name="TextureSizes"></a>
## Texture dimension sizes

Ideally, Texture dimension sizes should be powers of two on each side (that is, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048 pixels (px), and so on). The Textures do not have to be square; that is the width can be different from height. 
Note that specific platforms may impose maximum Texture dimension sizes. For DirectX, the maximum Texture sizes for different feature levels are as follows:

| Graphics APIs / Feature levels| Maximum 2D and Cubemap texture dimension size (px) |
|:---|:---| 
| DX9 Shader Model 2 (PC GPUs before 2004) / OpenGL ES 2.0| 2048 |
| DX9 Shader Model 3 (PC GPUs before 2006) / Windows Phone DX11 9.3 level / OpenGL ES 3.0| 4096 |
| DX10 Shader Model 4 / GL3 (PC GPUs before 2007) / OpenGL ES 3.1| 8192 |
| DX11 Shader Model 5 / GL4 (PC GPUs since 2008)| 16384 |

**Notes:**

* The Texture Importer only allows you to choose dimension sizes up to 8K (that is 8192 x 8192 px). 
* Mali-Txxx GPUs (See [Wikipedia](https://en.wikipedia.org/wiki/Mali_(GPU))) and OpenGL ES 3.1 ([www.opengl.org](http://www.opengl.org)) only support up to 4096px Texture dimension size for cubemaps.

It is possible to use NPOT (non-power of two) Texture sizes with Unity; however, NPOT Texture sizes generally take slightly more memory and might be slower for the GPU to sample, so it’s better for performance to use power of two sizes whenever you can. If the platform or GPU does not support NPOT Texture sizes, Unity scales and pads the Texture up to the next power of two size. This process uses more memory and makes loading slower (especially on older mobile devices). In general, you should only use NPOT sizes for GUI purposes.

You can scale up NPOT Texture Assets at import time using the __Non Power of 2__ option in the __Advanced__ section of the Texture Importer.

<a name="UVmapping"></a>
## UV mapping

When mapping a 2D Texture onto a 3D model, your 3D modelling application does a type of wrapping called UV mapping. Inside Unity, you can scale and move the Texture using [Materials](class-Material). Scaling normal and detail maps is especially useful.

<a name="Mipmaps"></a>
## Mip maps

Mip maps are lists of progressively smaller versions of an image, used to optimise performance on real-time 3D engines. Objects that are far away from the Camera use smaller Texture versions. Using mip maps uses 33% more memory, but not using them can result in a huge performance loss. You should always use mip maps for in-game [Textures](Textures); the only exceptions are Textures that are made smaller (for example, GUI textures, [Skybox](class-Skybox), Cursors and Cookies). Mip maps are also essential for avoiding many forms of Texture aliasing and shimmering.

<a name="Normalmaps"></a>
## Normal maps

Normal maps are used by normal map Shaders to make low-polygon models look as if they contain more detail. Unity uses normal maps encoded as RGB images. You also have the option to generate a normal map from a grayscale height map image.

<a name="Detailmaps"></a>
## Detail maps

If you want to make a Terrain, you normally use your main Texture to show areas of terrain such as grass, rocks and sand. If your terrain is large, it may end up very blurry. Detail Textures hide this fact by fading in small details as your main Texture gets closer.

When drawing Detail Textures, a neutral gray is invisible, white makes the main Texture twice as bright, and black makes the main Texture completely black.

See documentation on [Secondary Maps (Detail Maps)](StandardShaderMaterialParameterDetail) for more information.

<a name="Reflections"></a>
## Reflections (cubemaps)

To use a Texture for reflection maps (for example, in [Reflection Probes](class-ReflectionProbe) or a cubemapped [Skybox](class-Skybox), set the __Texture Shape__ to __Cube__. See documentation on [Cubemap Textures](class-Cubemap) for more information.

<a name="AnisotropicFiltering"></a>
## Anisotropic filtering

Anisotropic filtering increases Texture quality when viewed from a grazing angle. This rendering is resource-intensive on the graphics card. Increasing the level of Anisotropy is usually a good idea for ground and floor Textures. Use [Quality Settings](class-QualitySettings) to force anisotropic filtering for all Textures or disable it completely.

![Anisotropy used on the ground Texture {No anisotropy (left) | Maximum anisotropy (right)}  ](../uploads/Main/ImportingTextures-AnisoFiltering.png)
