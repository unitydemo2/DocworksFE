# Working with linear Textures

sRGB sampling allows the Unity Editor to render Shaders in linear color space when Textures are in gamma color space. When you select to work in linear color space, the Editor defaults to using sRGB sampling. If your [Textures](Textures) are in linear color space, you need to work in linear color space and disable sRGB sampling for each Texture. To learn how to do this, see [Disabling sRGB sampling](#DisablingsRGBSampling), below.

For further reading, see documentation on:

* [Linear rendering overview](LinearLighting) for background information on linear and gamma color space.
* [Linear or gamma workflow](LinearRendering-LinearOrGammaWorkflow) for information on selecting to work in linear or gamma color space.
* [Gamma Textures with linear rendering](LinearRendering-GammaTextures) for information on gamma Textures in a linear workflow.

## Legacy GUI

Rendering of elements of the[ Legacy GUI System](http://docs.unity3d.com/Manual/GUIScriptingGuide.html) is always done in gamma space. This means that for the legacy GUI system, Textures with their __Texture Type__ set to __Editor GUI and Legacy GUI__ do not have their gamma removed on import.

## Linear authored Textures

It is also important that lookup Textures, masks, and other textures with RGB values that mean something specific and have no gamma correction applied to them bypass sRGB sampling. This prevents values from the sampled Texture having non-existent gamma correction removed before they are used in the Shader, with calculations made with the same value as is stored on disk. Unity assumes that GUI textures and normal map textures are authored in a linear space.

<a name="DisablingsRGBSampling"> </a>
## Disabling sRGB sampling

To ensure a Texture is imported as a linear color space image, in the [Inspector window](UsingTheInspector) for the Texture:

* Select the appropriate __Texture Type__ for the Texture’s intended use.

* Uncheck __sRGB (Color Texture)__ if it is shown.

![The Inspector window for a Texture. Note the setting for __sRGB (Color Texture)__ is unchecked. This ensures the Texture is imported as a linear color space image](../uploads/Main/LinearRendering-SRGBSetting.png)