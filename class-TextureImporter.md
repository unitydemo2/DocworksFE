# Textures

Textures are image or movie files that lay over or wrap around your GameObjects to give them a visual effect. This page details the properties you need to manage for your Textures.

Unity recognises any image or movie file in a 3D project’s _Assets_ folder as a Texture (in 2D projects, they are saved as Sprites). As long as the image meets the size requirements specified below, it is imported and optimized for game use (although any Shaders you use for your GameObjects have specific Texture requirements). This extends to multi-layer Photoshop or TIFF files, which are automatically flattened on import so that there is no size penalty for your game. This flattening happens internally to Unity, not to the PSD file itself, and is optional, so you can continue to save and import your PSD files with layers intact.

## Properties

![The Texture Inspector window](../uploads/Main/TextureImporter55.png)

The Inspector window is split into two sections: the __Texture Importer__ above, and the __Preview__ below.

## Texture Importer

The Texture Importer defines how images are imported from your project’s _Assets_ folder into the Unity Editor. To access the Texture Importer, select the image file in the Project window. The Texture Importer opens in the Inspector window.

Note that some of the less commonly used properties are hidden by default. Click __Advanced__ in the Inspector window to view these.

The first property in the Texture Importer is the __Texture Type__. Use this to select the type of Texture you want to create from the source image file. See documentation on [Texture types](TextureTypes) for more information on each type.

| **Property:** | **Function:** |
|:---|:---| 
| __Texture Type__| Use this to define what your Texture is to be used for. The other properties in the Texture Importer change depending on which one you choose. |
|&nbsp;&nbsp;&nbsp;&nbsp;Default | This is the most common setting used for all Textures. It provides access to most of the properties for Texture importing. |
|&nbsp;&nbsp;&nbsp;&nbsp;Normal Map | Select this to turn the color channels into a format suitable for real-time normal mapping. See [Importing Textures](ImportingTextures) for more information on normal mapping.
|&nbsp;&nbsp;&nbsp;&nbsp;Editor GUI | Select this if you are using the Texture on any HUD or GUI controls. |
|&nbsp;&nbsp;&nbsp;&nbsp;Sprite (2D and UI) | Select this if you are using the Texture in a 2D game as a [Sprite](Sprites). 
|&nbsp;&nbsp;&nbsp;&nbsp;Cursor | Select this if you are using the Texture as a custom cursor. |
|&nbsp;&nbsp;&nbsp;&nbsp;Cookie | Select this to set your Texture up with the basic parameters used for the [Cookies](Cookies) of your Scene’s [Lights](class-Light). |
|&nbsp;&nbsp;&nbsp;&nbsp;Lightmap | Select this if you are using the Texture as a [Lightmap](LightmapParameters). This option enables encoding into a specific format (RGBM or dLDR, depending on the platform) and a post-processing step on Texture data (a push-pull dilation pass).  |
|&nbsp;&nbsp;&nbsp;&nbsp;Single Channel | Select this if you only need one channel in the Texture. |


The second property in the Texture Importer is the __Texture Shape__. Use this to select and define the shape and structure of the Texture.

| **Property:** | **Function:** |
|:---|:---|:---| 
| __Texture Shape__  | Use this to define the shape of the Texture. This is set to 2D by default.|
|&nbsp;&nbsp;&nbsp;&nbsp;2D | This is the most common setting for all Textures; it defines the image file as a 2D Texture. These are used to map textures to 3D meshes and GUI elements, among other project elements. |
|&nbsp;&nbsp;&nbsp;&nbsp;Cube | This defines the Texture as a cubemap. You could use this for Skyboxes or Reflection Probes, for example. Selecting __Cube__ displays different mapping options. |
| __Mapping__ | This setting is only available when __Texture Shape__ is set to __Cube__. Use __Mapping__ to specify how the Texture is projected onto your GameObject. This is set to __Auto__ by default.|
|&nbsp;&nbsp;&nbsp;&nbsp;Auto | Unity tries to automatically work out the layout from the Texture information. |
|&nbsp;&nbsp;&nbsp;&nbsp;6 Frames Layout (Cubic Environment) | The Texture contains six images arranged in one of the standard cubemap layouts: cross, or sequence (+x -x +y -y +z -z). The   images can be orientated either horizontally or vertically. |
|&nbsp;&nbsp;&nbsp;&nbsp;Latitude Longitude (Cylindrical) | Maps the Texture to a 2D Latitude-Longitude representation. |
|&nbsp;&nbsp;&nbsp;&nbsp;Mirrored Ball (Sphere Mapped) | Maps the Texture to a sphere-like cubemap. |
| __Convolution Type__ | Choose the type of pre-convolution (that is, filtering) that you want to use for this texture. The result of pre-convolution is stored in mips. This is set to __None__ by default. |
|&nbsp;&nbsp;&nbsp;&nbsp;None | The Texture has no pre-convolution (no filtering). |
|&nbsp;&nbsp;&nbsp;&nbsp;Specular (Glossy Reflection) | Select this to use cubemaps as Reflection Probes. The Texture mip maps are pre-convoluted (filtered)  with the engine BRDF. (See Wikipedia's page on [Bidirectional reflectance distribution function](https://en.wikipedia.org/wiki/Bidirectional_reflectance_distribution_function) for more information.) |
|&nbsp;&nbsp;&nbsp;&nbsp;Diffuse (Irradiance) | The Texture is convoluted (filtered)  to represent irradiance. This is useful if you use the cubemap as a Light Probe. |
| __Fixup Edge Seams__  | This option is only available with the __None__ or __Diffuse__ convolution (filter). Use this on low-end platforms as a work-around for filtering limitations, such as cubemaps incorrectly filtered between faces. |


## Platform-specific overrides

The Texture Inspector window has a __Platform-specific overrides__ panel.

![__Platform-specific overrides__ panel](../uploads/Main/PlatformSpecificOverrides.png)

When building for different platforms, you need to think about the resolution, the file size with associated memory size requirements, the pixel dimensions, and the quality of your Textures for each target platform. Use the __Platform-specific overrides__ panel to set default options (using __Default__), and then override them for a specific platform using the buttons along the top of the panel. 

| **Property:** | **Function:** |
|:---|:---| 
| __Max Size__ | The maximum imported Texture dimensions in pixels. Artists often prefer to work with huge dimension-size Textures; use __Max Size__ to scale the Texture down to a suitable dimension-size. |
| __Compression__ | Choose the compression type for the Texture. This parameter helps the system choose the right compression format for a Texture. Depending on the platform and the availability of compression formats, different settings might end up with the same internal format (for example, __Low Quality Compression__ has an effect on mobile platforms, but not on desktop platforms). |
|&nbsp;&nbsp;&nbsp;&nbsp;None | The Texture is not compressed. |
|&nbsp;&nbsp;&nbsp;&nbsp;Low Quality | The Texture is compressed in a low-quality format. This results in a lower memory usage compared with __Normal Quality__.|
|&nbsp;&nbsp;&nbsp;&nbsp;Normal Quality | The Texture is compressed with a standard format. |
|&nbsp;&nbsp;&nbsp;&nbsp;High Quality | The Texture is compressed in a high-quality format. This results in a higher memory usage compared with __Normal Quality__. |
| __Format__ | This bypasses the automatic system to specify what internal representation is used for the Texture. The list of available formats depends on the platform and Texture type. See documentation on [Texture formats for platform-specific overrides](class-TextureImporterOverride) for more information. <br/>**Note:** Even when a platform is not overridden, this option shows the format chosen by the automatic system. The Format property is only available when overriding for a specific platform, and not as a default setting. |
| __Use crunch compression__ | Use crunch compression, if applicable. Crunch is a lossy compression format on top of DXT Texture compression. Textures are decompressed to DXT on the CPU and then uploaded on the GPU at runtime. Crunch compression helps the Texture use the lowest possible amount of space on disk and for downloads. Crunch Textures can take a long time to compress, but decompression at runtime is very fast.|
| __Compressor Quality__ | When using Crunch Texture compression, use the slider to adjust the quality. A higher compression quality means larger Textures and longer compression times. 

