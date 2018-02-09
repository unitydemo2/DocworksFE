# Accessing shader properties in Cg/HLSL


Shader declares Material properties in a [Properties](SL-Properties) block. If you want to access some of those properties in a [shader program](SL-ShaderPrograms), you need to declare a Cg/HLSL variable with the same name and a matching type. An example is provided in [Shader Tutorial: Vertex and Fragment Programs](ShaderTut2).

For example these shader properties:


````
_MyColor ("Some Color", Color) = (1,1,1,1) 
_MyVector ("Some Vector", Vector) = (0,0,0,0) 
_MyFloat ("My float", Float) = 0.5 
_MyTexture ("Texture", 2D) = "white" {} 
_MyCubemap ("Cubemap", CUBE) = "" {} 
````

would be declared for access in Cg/HLSL code as:


````
fixed4 _MyColor; // low precision type is usually enough for colors
float4 _MyVector;
float _MyFloat; 
sampler2D _MyTexture;
samplerCUBE _MyCubemap;
````

Cg/HLSL can also accept __uniform__ keyword, but it is not necessary:


````
uniform float4 _MyColor;
````

Property types in ShaderLab map to Cg/HLSL variable types this way:

* Color and Vector properties map to __float4__, __half4__ or __fixed4__ variables.
* Range and Float properties map to __float__, __half__ or __fixed__ variables.
* Texture properties map to __sampler2D__ variables for regular (2D) textures; Cubemaps map to __samplerCUBE__; and 3D textures map to __sampler3D__.


## How property values are provided to shaders

Shader property values are found and provided to shaders from these places:

* Per-Renderer values set in [MaterialPropertyBlock](ScriptRef:MaterialPropertyBlock.html). This is typically "per-instance" data (e.g. customized tint color for a lot of objects that all share the same material).
* Values set in the [Material](class-Material) that's used on the rendered object.
* Global shader properties, set either by Unity rendering code itself (see [built-in shader variables](SL-UnityShaderVariables)), or from your own scripts (e.g. [Shader.SetGlobalTexture](ScriptRef:Shader.SetGlobalTexture.html)).

The order of precedence is like above: per-instance data overrides everything; then Material data is used; and finally if shader property does not exist in these two places then global property value is used. Finally, if there's no shader property value defined anywhere, then "default" (zero for floats, black for colors, empty white texture for textures) value will be provided.


## Serialized and Runtime Material properties

[Materials](class-Material) can contain both serialized and runtime-set property values.

Serialized data is all the properties defined in shader's [Properties](SL-Properties) block. Typically these are values that need to be stored in the material, and are tweakable by the user in Material Inspector.

A material can also have some properties that are used by the shader, but not declared in shader's [Properties](SL-Properties) block. Typically this is for properties that are set from script code at runtime, e.g. via [Material.SetColor](ScriptRef:Material.SetColor.html). Note that matrices and arrays can only exist as non-serialized runtime properties (since there's no way to define them in Properties block).


## Special Texture properties

For each texture that is setup as a shader/material property, Unity also sets up some extra information in additional vector properties.


#### Texture tiling & offset

[Materials](class-Material) often have Tiling and Offset fields for their texture properties. This information is passed into shaders in a float4 _{TextureName}_`_ST` property:

* `x` contains X tiling value
* `y` contains Y tiling value
* `z` contains X offset value
* `w` contains Y offset value

For example, if a shader contains texture named `_MainTex`, the tiling information will be in a `_MainTex_ST` vector.


#### Texture size

_{TextureName}_`_TexelSize` - a float4 property contains texture size information:

* `x` contains 1.0/width
* `y` contains 1.0/height
* `z` contains width
* `w` contains height


#### Texture HDR parameters

_{TextureName}_`_HDR` - a float4 property with information on how to decode a potentially HDR (e.g. RGBM-encoded) texture depending on the [color space](LinearLighting) used. See `DecodeHDR` function in [UnityCG.cginc](SL-BuiltinIncludes) shader include file.


## Color spaces and color/vector shader data

When using [Linear color space](LinearLighting), all material color properties are supplied as sRGB colors, but are converted into linear values when passed into shaders.

For example, if your [Properties](SL-Properties) shader block contains a `Color` property called "_MyColor", then the corresponding "_MyColor" HLSL variable will get the linear color value.

For properties that are marked as `Float` or `Vector` type, no color space conversions are done by default; it is assumed that they contain non-color data. It is possible to add `[Gamma]` attribute for float/vector properties to indicate that they are specified in sRGB space, just like colors (see [Properties](SL-Properties)).


## See Also

* [ShaderLab Properties block](SL-Properties).
* [Writing Shader Programs](SL-ShaderPrograms).
