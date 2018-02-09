#ShaderLab: Properties

Shaders can define a list of parameters to be set by artists in Unity's [material inspector](Materials).
The Properties block in the [shader file](SL-Shader) defines them.

##Syntax


#### Properties
````
Properties { Property [Property ...] }
````
Defines the property block. Inside braces multiple properties are defined as follows.


#### Numbers and Sliders
````
name ("display name", Range (min, max)) = number
name ("display name", Float) = number
name ("display name", Int) = number
````
These all defines a number (scalar) property with a default value. The `Range` form makes it be displayed
as a slider between *min* and *max* ranges.


#### Colors and Vectors
````
name ("display name", Color) = (number,number,number,number)
name ("display name", Vector) = (number,number,number,number)
````
Defines a color property with default value of given RGBA components, or a 4D vector property with a default value.
Color properties have a color picker shown for them, and are adjusted as needed depending on the color space (see [Properties in Shader Programs](SL-PropertiesInPrograms)). Vector properties are displayed as four number fields.


#### Textures
````
name ("display name", 2D) = "defaulttexture" {}
name ("display name", Cube) = "defaulttexture" {}
name ("display name", 3D) = "defaulttexture" {}
````
Defines a [2D texture](class-TextureImporter), [cubemap](class-Cubemap) or [3D (volume)](class-Texture3D) property respectively.



## Details

Each property inside the shader is referenced by **name** (in Unity, it's common to start shader property names with underscore). The property will show up in material inspector as **display name**. For each property a default value is given after equals sign:

* For _Range_ and _Float_ properties it's just a single number, for example "13.37".
* For _Color_ and _Vector_ properties it's four numbers in parentheses, for example "(1,0.5,0.2,1)".
* For 2D Textures, the default value is either an empty string, or one of the built-in default Textures: "white" (RGBA: 1,1,1,1), "black" (RGBA: 0,0,0,0), "gray" (RGBA: 0.5,0.5,0.5,0.5), "bump" (RGBA: 0.5,0.5,1,0.5) or "red" (RGBA: 1,0,0,0).
* For non-2D Textures (Cube, 3D, 2DArray) the default value is an empty string. When a Material does not have a Cubemap/3D/Array Texture assigned, a gray one (RGBA: 0.5,0.5,0.5,0.5) is used.

Later on in the shader's fixed function parts, property values can be accessed using property name in
square brackets: **[name]**. For example, you could make blending mode be driven by a material property by declaring two integer
properties (say "_SrcBlend" and "_DstBlend"), and later on make [Blend Command](SL-Blend) use them: `Blend [_SrcBlend] [_DstBlend]`.

Shader parameters that are in the `Properties` block are serialized as [Material](Materials) data.
[Shader programs](SL-ShaderPrograms) can actually have more parameters (like matrices, vectors and floats) that
are set on the material from code at runtime, but if they are not part of the Properties block then their values will not be saved.
This is mostly useful for values that are completely script code-driven (using [Material.SetFloat](ScriptRef:Material.SetFloat.html) and similar functions).


### Property attributes and drawers

In front of any property, optional attributes in square brackets can be specified. These are
either attributes recognized by Unity, or they can indicate your own
[MaterialPropertyDrawer classes](ScriptRef:MaterialPropertyDrawer.html) to control how they should be
rendered in the [material inspector](class-Material). Attributes recognized by Unity:

* `[HideInInspector]` - does not show the property value in the material inspector.
* `[NoScaleOffset]` - material inspector will not show texture tiling/offset fields for texture properties with this attribute.
* `[Normal]` - indicates that a texture property expects a normal-map.
* `[HDR]` - indicates that a texture property expects a high-dynamic range (HDR) texture.
* `[Gamma]` - indicates that a float/vector property is specified as sRGB value in the UI (just like colors are), and possibly needs conversion according to color space used. See [Properties in Shader Programs](SL-PropertiesInPrograms).
* `[PerRendererData]` - indicates that a texture property will be coming from per-renderer data
   in the form of a [MaterialPropertyBlock](ScriptRef:MaterialPropertyBlock.html). Material inspector changes the texture
   slot UI for these properties.


## Example

````
// properties for a water shader
Properties
{
    _WaveScale ("Wave scale", Range (0.02,0.15)) = 0.07 // sliders
    _ReflDistort ("Reflection distort", Range (0,1.5)) = 0.5
    _RefrDistort ("Refraction distort", Range (0,1.5)) = 0.4
    _RefrColor ("Refraction color", Color) = (.34, .85, .92, 1) // color
    _ReflectionTex ("Environment Reflection", 2D) = "" {} // textures
    _RefractionTex ("Environment Refraction", 2D) = "" {}
    _Fresnel ("Fresnel (A) ", 2D) = "" {}
    _BumpMap ("Bumpmap (RGB) ", 2D) = "" {}
}
````


## Texture property options (removed in 5.0)

Before Unity 5, texture properties could have options inside the curly brace block, e.g. `TexGen CubeReflect`.
These were controlling fixed function texture coordinate generation. This functionality was removed in 5.0;
if you need texgen you should write a [vertex shader](SL-ShaderPrograms) instead.
See [Implementing Fixed Function TexGen page](SL-ImplementingTexGen) page for examples.


## See Also

* [Accessing Shader Properties in HLSL/Cg](SL-PropertiesInPrograms).
* [Material Property Drawers](ScriptRef:MaterialPropertyDrawer.html).
