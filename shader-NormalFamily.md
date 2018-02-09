Normal Shader Family
====================

**Note.** Unity 5 introduced the [Standard Shader](shader-StandardShader) which replaces these shaders.

These shaders are the basic shaders in Unity. They are not specialized in any way and should be suitable for most opaque objects. They are not suitable if you want your object to be transparent, emitting light etc. 

[Vertex Lit](shader-NormalVertexLit)
------------------------------------


![shader-NormalVertexLit](../uploads/Shaders/Thumb-NormalVertex.png)

**Assets needed:**

* One __Base__ texture, no alpha channel required


[Diffuse](shader-NormalDiffuse)
-------------------------------


![shader-NormalDiffuse](../uploads/Shaders/Thumb-NormalDiffuse.png)

**Assets needed:**

* One __Base__ texture, no alpha channel required


[Specular](shader-NormalSpecular)
---------------------------------


![shader-NormalSpecular](../uploads/Shaders/Thumb-NormalSpec.png)

**Assets needed:**

* One __Base__ texture with alpha channel for Specular Map


[Normal mapped](shader-NormalBumpedDiffuse)
-------------------------------------------


![shader-NormalBumpedDiffuse](../uploads/Shaders/Thumb-NormalBump.png)

**Assets needed:**

* One __Base__ texture, no alpha channel required
* One __Normal map__


[Normal mapped Specular](shader-NormalBumpedSpecular)
-----------------------------------------------------


![shader-NormalBumpedSpecular](../uploads/Shaders/Thumb-NormalBumpSpec.png)

**Assets needed:**

* One __Base__ texture with alpha channel for Specular Map
* One __Normal map__


[Parallax](shader-NormalParallaxDiffuse)
----------------------------------------


![shader-NormalParallaxDiffuse](../uploads/Shaders/Thumb-NormalParallaxBump.png)

**Assets needed:**

* One __Base__ texture, no alpha channel required
* One __Normal map__
* One __Height__ texture with Parallax Depth in the alpha channel


[Parallax Specular](shader-NormalParallaxSpecular)
--------------------------------------------------


![shader-NormalParallaxSpecular](../uploads/Shaders/Thumb-NormalParallaxBumpSpec.png)

**Assets needed:**

* One __Base__ texture with alpha channel for Specular Map
* One __Normal map__
* One __Height__ texture with Parallax Depth in the alpha channel


[Decal](shader-NormalDecal)
---------------------------


![shader-NormalDecal](../uploads/Shaders/Thumb-NormalDecal.png)

**Assets needed:**

* One __Base__ texture, no alpha channel required
* One __Decal__ texture with alpha channel for Decal transparency


[Diffuse Detail](shader-NormalDiffuseDetail)
--------------------------------------------


![shader-NormalDiffuseDetail](../uploads/Shaders/Thumb-NormalDiffuseDetail.png)

**Assets needed:**

* One __Base__ texture, no alpha channel required
* One __Detail__ grayscale texture; with 50% gray being neutral color
