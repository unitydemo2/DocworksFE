#Materials, Shaders & Textures

Rendering in Unity uses **Materials**, **Shaders** and **Textures**. All three have a close relationship.

* **Materials** define how a surface should be rendered, by including references to the Textures it uses, tiling information, Color tints and more. The available options for a Material depend on which Shader the Material is using.

* **Shaders** are small scripts that contain the mathematical calculations and algorithms for calculating the Color of each pixel rendered, based on the lighting input and the Material configuration.

* **Textures** are bitmap images. A Material can contain references to textures, so that the Material's Shader can use the textures while calculating the surface color of a GameObject. In addition to basic Color (Albedo) of a GameObject's surface, Textures can represent many other aspects of a Material's surface such as its reflectivity or roughness.

A Material specifies one specific Shader to use, and the Shader used determines which options are available in the Material. A Shader specifies one or more Texture variables that it expects to use, and the Material Inspector in Unity allows you to assign your own Texture Assets to these Texture variables.

For most normal rendering (such as rendering characters, scenery, environments, solid and transparent GameObjects, hard and soft surfaces) the [Standard Shader](shader-StandardShader) is usually the best choice. This is a highly customisable shader which is capable of rendering many types of surface in a highly realistic way. 

There are other situations where a different built-in Shader, or even a custom written shader might be appropriate (for example liquids, foliage, refractive glass, particle effects, cartoony, illustrative or other artistic effects, or other special effects like night vision, heat vision or x-ray vision). 

For more information, see the following pages:

* [Creating and Using Materials](Materials)
* [The Built-in Standard Shader](shader-StandardShader)
* [Other built-in Shaders](Built-inShaderGuide)
* [Writing Your Own Shaders](ShadersOverview)

---

* <span class="page-history">2017-10-26 New page</span>

* <span class="page-edit">2017-10-26 <!-- include IncludeTextAmendPageSomeEdit --></span>

