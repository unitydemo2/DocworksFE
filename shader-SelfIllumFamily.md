Self-Illuminated Shader Family
==============================

**Note.** Unity 5 introduced the [Standard Shader](shader-StandardShader) which replaces these shaders.

The __Self-Illuminated__ shaders will emit light only onto themselves based on an attached alpha channel. They do not require any Lights to shine on them to emit this light. Any vertex lights or pixel lights will simply add more light on top of the self-illumination.

This is mostly used for light emitting objects. For example, parts of the wall texture could be self-illuminated to simulate lights or displays. It can also be useful to light power-up objects that should always have consistent lighting throughout the game, regardless of the lights shining on it.

[Self-Illuminated Vertex-Lit](shader-SelfIllumVertexLit)
--------------------------------------------------------


![shader-SelfIllumVertexLit](../uploads/Shaders/Thumb-IllumVertex.png)

**Assets needed:**

* One __Base__ texture, no alpha channel required
* One __Illumination__ texture with alpha channel for Illumination Map

[&#187; More details](shader-SelfIllumVertexLit)


[Self-Illuminated Diffuse](shader-SelfIllumDiffuse)
---------------------------------------------------


![shader-SelfIllumDiffuse](../uploads/Shaders/Thumb-IllumDiffuse.png)

**Assets needed:**

* One __Base__ texture, no alpha channel required
* One __Illumination__ texture with alpha channel for Illumination Map

[&#187; More details](shader-SelfIllumDiffuse)


[Self-Illuminated Specular](shader-SelfIllumSpecular)
-----------------------------------------------------


![shader-SelfIllumSpecular](../uploads/Shaders/Thumb-IllumSpec.png)

**Assets needed:**

* One __Base__ texture with alpha channel for Specular Map
* One __Illumination__ texture with alpha channel for Illumination Map

[&#187; More details](shader-SelfIllumSpecular)


[Self-Illuminated Bumped](shader-SelfIllumBumpedDiffuse)
--------------------------------------------------------


![shader-SelfIllumBumpedDiffuse](../uploads/Shaders/Thumb-IllumBump.png)

**Assets needed:**

* One __Base__ texture, no alpha channel required
* One __Normal map__ normal map with alpha channel for Illumination

[&#187; More details](shader-SelfIllumBumpedDiffuse)


[Self-Illuminated Bumped Specular](shader-SelfIllumBumpedSpecular)
------------------------------------------------------------------


![shader-SelfIllumBumpedSpecular](../uploads/Shaders/Thumb-IllumBumpSpec.png)

**Assets needed:**

* One __Base__ texture with alpha channel for Specular Map
* One __Normal map__ normal map with alpha channel for Illumination Map

[&#187; More details](shader-SelfIllumBumpedSpecular)


[Self-Illuminated Parallax](shader-SelfIllumParallaxDiffuse)
------------------------------------------------------------


![shader-SelfIllumParallaxDiffuse](../uploads/Shaders/Thumb-IllumParallaxBump.png)

**Assets needed:**

* One __Base__ texture, no alpha channel required
* One __Normal map__ normal map with alpha channel for Illumination Map & Parallax Depth combined

**Note:**
One consideration of this shader is that the __Bumpmap__ texture's alpha channel doubles as a Illumination and the Parallax Depth.

[&#187; More details](shader-SelfIllumParallaxDiffuse)


[Self-Illuminated Parallax Specular](shader-SelfIllumParallaxSpecular)
----------------------------------------------------------------------


![shader-SelfIllumParallaxSpecular](../uploads/Shaders/Thumb-IllumParallaxBumpSpec.png)

**Assets needed:**

* One __Base__ texture with alpha channel for Specular Map
* One __Normal map__ normal map with alpha channel for Illumination Map & Parallax Depth combined

**Note:**
One consideration of this shader is that the __Bumpmap__ texture's alpha channel doubles as a Illumination and the Parallax Depth.

[&#187; More details](shader-SelfIllumParallaxSpecular)
