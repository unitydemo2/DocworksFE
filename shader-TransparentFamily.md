Transparent Shader Family
=========================

**Note.** Unity 5 introduced the [Standard Shader](shader-StandardShader) which replaces these shaders.

The Transparent shaders are used for fully- or semi-transparent objects. Using the alpha channel of the __Base__ texture, you can determine areas of the object which can be more or less transparent than others. This can create a great effect for glass, HUD interfaces, or sci-fi effects.

[Transparent Vertex-Lit](shader-TransVertexLit)
-----------------------------------------------


![shader-TransVertexLit](../uploads/Shaders/Thumb-TransVertex.png)

**Assets needed:**

* One __Base__ texture with alpha channel for Transparency Map

[&#187; More details](shader-TransVertexLit)


[Transparent Diffuse](shader-TransDiffuse)
------------------------------------------


![shader-TransDiffuse](../uploads/Shaders/Thumb-TransDiffuse.png)

**Assets needed:**

* One __Base__ texture with alpha channel for Transparency Map

[&#187; More details](shader-TransDiffuse)


[Transparent Specular](shader-TransSpecular)
--------------------------------------------


![shader-TransSpecular](../uploads/Shaders/Thumb-TransSpec.png)

**Assets needed:**

* One __Base__ texture with alpha channel for combined Transparency Map/Specular Map

**Note:**
One limitation of this shader is that the __Base__ texture's alpha channel doubles as a Specular Map for the Specular shaders in this family.


[&#187; More details](shader-TransSpecular)


[Transparent Normal mapped](shader-TransBumpedDiffuse)
------------------------------------------------------


![shader-TransBumpedDiffuse](../uploads/Shaders/Thumb-TransBump.png)

**Assets needed:**

* One __Base__ texture with alpha channel for Transparency Map
* One __Normal map__ normal map, no alpha channel required

[&#187; More details](shader-TransBumpedDiffuse)


[Transparent Normal mapped Specular](shader-TransBumpedSpecular)
----------------------------------------------------------------


![shader-TransBumpedSpecular](../uploads/Shaders/Thumb-TransBumpSpec.png)

**Assets needed:**

* One __Base__ texture with alpha channel for combined Transparency Map/Specular Map
* One __Normal map__ normal map, no alpha channel required

**Note:**
One limitation of this shader is that the __Base__ texture's alpha channel doubles as a Specular Map for the Specular shaders in this family.

[&#187; More details](shader-TransBumpedSpecular)


[Transparent Parallax](shader-TransParallaxDiffuse)
---------------------------------------------------


![shader-TransParallaxDiffuse](../uploads/Shaders/Thumb-TransParallaxBump.png)

**Assets needed:**

* One __Base__ texture with alpha channel for Transparency Map
* One __Normal map__ normal map with alpha channel for Parallax Depth

[&#187; More details](shader-TransParallaxDiffuse)


[Transparent Parallax Specular](shader-TransParallaxSpecular)
-------------------------------------------------------------


![shader-TransParallaxSpecular](../uploads/Shaders/Thumb-TransParallaxBumpSpec.png)

**Assets needed:**

* One __Base__ texture with alpha channel for combined Transparency Map/Specular Map
* One __Normal map__ normal map with alpha channel for Parallax Depth

**Note:**
One limitation of this shader is that the __Base__ texture's alpha channel doubles as a Specular Map for the Specular shaders in this family.

[&#187; More details](shader-TransParallaxSpecular)
