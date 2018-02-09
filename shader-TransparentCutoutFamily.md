Transparent Cutout Shader Family
================================

**Note.** Unity 5 introduced the [Standard Shader](shader-StandardShader) which replaces these shaders.

The Transparent Cutout shaders are used for objects that have fully opaque and fully transparent parts (no partial transparency). Things like chain fences, trees, grass, etc.

[Transparent Cutout Vertex-Lit](shader-TransCutVertexLit)
---------------------------------------------------------


![shader-TransCutVertexLit](../uploads/Shaders/Thumb-TransCutoutVertex.png)

**Assets needed:**

* One __Base__ texture with alpha channel for Transparency Map

[&#187; More details](shader-TransCutVertexLit)


[Transparent Cutout Diffuse](shader-TransCutDiffuse)
----------------------------------------------------


![shader-TransCutDiffuse](../uploads/Shaders/Thumb-TransCutoutDiffuse.png)

**Assets needed:**

* One __Base__ texture with alpha channel for Transparency Map

[&#187; More details](shader-TransCutDiffuse)


[Transparent Cutout Specular](shader-TransCutSpecular)
------------------------------------------------------


![shader-TransCutSpecular](../uploads/Shaders/Thumb-TransCutoutSpec.png)

**Assets needed:**

* One __Base__ texture with alpha channel for combined Transparency Map/Specular Map

**Note:**
One limitation of this shader is that the __Base__ texture's alpha channel doubles as a Specular Map for the Specular shaders in this family.

[&#187; More details](shader-TransCutSpecular)


[Transparent Cutout Bumped](shader-TransCutBumpedDiffuse)
---------------------------------------------------------


![shader-TransCutBumpedDiffuse](../uploads/Shaders/Thumb-TransCutoutBump.png)

**Assets needed:**

* One __Base__ texture with alpha channel for Transparency Map
* One __Normal map__ normal map, no alpha channel required

[&#187; More details](shader-TransCutBumpedDiffuse)


[Transparent Cutout Bumped Specular](shader-TransCutBumpedSpecular)
-------------------------------------------------------------------


![shader-TransCutBumpedSpecular](../uploads/Shaders/Thumb-TransCutoutBumpSpec.png)

**Assets needed:**

* One __Base__ texture with alpha channel for combined Transparency Map/Specular Map
* One __Normal map__ normal map, no alpha channel required

**Note:**
One limitation of this shader is that the __Base__ texture's alpha channel doubles as a Specular Map for the Specular shaders in this family.

[&#187; More details](shader-TransCutBumpedSpecular)
