Reflective Shader Family
========================

**Note.** Unity 5 introduced the [Standard Shader](shader-StandardShader) which replaces these shaders.

__Reflective__ shaders will allow you to use a Cubemap which will be reflected on your mesh. You can also define areas of more or less reflectivity on your object through the alpha channel of the __Base__ texture. High reflectivity is a great effect for glosses, oils, chrome, etc. Low reflectivity can add effect for metals, liquid surfaces, or video monitors.

[Reflective Vertex-Lit](shader-ReflectiveVertexLit)
---------------------------------------------------


![shader-ReflectiveVertexLit](../uploads/Shaders/Thumb-ReflVertex.png)

**Assets needed:**

* One __Base__ texture with alpha channel for defining reflective areas
* One __Reflection__ Cubemap for Reflection Map

[&#187; More details](shader-ReflectiveVertexLit)


[Reflective Diffuse](shader-ReflectiveDiffuse)
----------------------------------------------


![shader-ReflectiveDiffuse](../uploads/Shaders/Thumb-ReflDiffuse.png)

**Assets needed:**

* One __Base__ texture with alpha channel for defining reflective areas
* One __Reflection__ Cubemap for Reflection Map

[&#187; More details](shader-ReflectiveDiffuse)


[Reflective Specular](shader-ReflectiveSpecular)
------------------------------------------------


![shader-ReflectiveSpecular](../uploads/Shaders/Thumb-ReflSpec.png)

**Assets needed:**

* One __Base__ texture with alpha channel for defining reflective areas & Specular Map combined
* One __Reflection__ Cubemap for Reflection Map

**Note:**
One consideration for this shader is that the __Base__ texture's alpha channel will double as both the reflective areas and the Specular Map.

[&#187; More details](shader-ReflectiveSpecular)


[Reflective Normal mapped](shader-ReflectiveBumpedDiffuse)
----------------------------------------------------------


![shader-ReflectiveBumpedDiffuse](../uploads/Shaders/Thumb-ReflBump.png)

**Assets needed:**

* One __Base__ texture with alpha channel for defining reflective areas
* One __Reflection__ Cubemap for Reflection Map
* One __Normal map__, no alpha channel required

[&#187; More details](shader-ReflectiveBumpedDiffuse)


[Reflective Normal Mapped Specular](shader-ReflectiveBumpedSpecular)
--------------------------------------------------------------------


![shader-ReflectiveBumpedSpecular](../uploads/Shaders/Thumb-ReflBumpSpec.png)

**Assets needed:**

* One __Base__ texture with alpha channel for defining reflective areas & Specular Map combined
* One __Reflection__ Cubemap for Reflection Map
* One __Normal map__, no alpha channel required

**Note:**
One consideration for this shader is that the __Base__ texture's alpha channel will double as both the reflective areas and the Specular Map.

[&#187; More details](shader-ReflectiveBumpedSpecular)


[Reflective Parallax](shader-ReflectiveParallaxDiffuse)
-------------------------------------------------------


![shader-ReflectiveParallaxDiffuse](../uploads/Shaders/Thumb-ReflParallaxBump.png)

**Assets needed:**

* One __Base__ texture with alpha channel for defining reflective areas
* One __Reflection__ Cubemap for Reflection Map
* One __Normal map__, with alpha channel for Parallax Depth

[&#187; More details](shader-ReflectiveParallaxDiffuse)


[Reflective Parallax Specular](shader-ReflectiveParallaxSpecular)
-----------------------------------------------------------------


![shader-ReflectiveParallaxSpecular](../uploads/Shaders/Thumb-ReflParallaxBumpSpec.png)

**Assets needed:**

* One __Base__ texture with alpha channel for defining reflective areas & Specular Map
* One __Reflection__ Cubemap for Reflection Map
* One __Normal map__, with alpha channel for Parallax Depth

**Note:**
One consideration for this shader is that the __Base__ texture's alpha channel will double as both the reflective areas and the Specular Map.

[&#187; More details](shader-ReflectiveParallaxSpecular)


[Reflective Normal mapped Unlit](shader-ReflectiveBumpedUnlit)
--------------------------------------------------------------


![shader-ReflectiveBumpedUnlit](../uploads/Shaders/Thumb-ReflBumpUnlit.png)

**Assets needed:**

* One __Base__ texture with alpha channel for defining reflective areas
* One __Reflection__ Cubemap for Reflection Map
* One __Normal map__, no alpha channel required

[&#187; More details](shader-ReflectiveBumpedUnlit)


[Reflective Normal mapped Vertex-Lit](shader-ReflectiveBumpedVertexLit)
-----------------------------------------------------------------------


![shader-ReflectiveBumpedVertexLit](../uploads/Shaders/Thumb-ReflBumpVertex.png)

**Assets needed:**

* One __Base__ texture with alpha channel for defining reflective areas
* One __Reflection__ Cubemap for Reflection Map
* One __Normal map__, no alpha channel required

[&#187; More details](shader-ReflectiveBumpedVertexLit)
