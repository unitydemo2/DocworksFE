Rendering with Replaced Shaders
===============================


Some rendering effects require rendering a scene with a different set of shaders. For example, good edge detection would need a texture with scene normals, so it could detect edges where surface orientations differ. Other effects might need a texture with scene depth, and so on. To achieve this, it is possible to render the scene with replaced shaders of all objects.

Shader replacement is done from scripting using [Camera.RenderWithShader](ScriptRef:Camera.RenderWithShader.html) or [Camera.SetReplacementShader](ScriptRef:Camera.SetReplacementShader.html) functions. Both functions take a __shader__ and a __replacementTag__.

It works like this: the camera renders the scene as it normally would. the objects still use their materials, but the actual shader that ends up being used is changed:

* If __replacementTag__ is empty, then all objects in the scene are rendered with the given replacement shader.
* If __replacementTag__ is not empty, then for each object that would be rendered:
    * The real object's shader is queried for the [tag value](SL-SubShaderTags).
    * If it does not have that tag, object is **not rendered**.
    * A [subshader](SL-SubShader) is found in the replacement shader that has a given tag with the found value. If no such subshader is found, object is **not rendered**.
    * Now that subshader is used to render the object.


So if all shaders would have, for example, a "RenderType" tag with values like "Opaque", "Transparent", "Background", "Overlay", you could write a replacement shader that only renders solid objects by using one subshader with RenderType=Solid [tag](SL-SubShaderTags). The other tag types would not be found in the replacement shader, so the objects would be not rendered. Or you could write several subshaders for different "RenderType" tag values. Incidentally, all built-in Unity shaders have a "RenderType" tag set.

Lit shader replacement
----------------------


When using shader replacement the scene is rendered using the render path that is configured on the camera. This means that the shader used for replacement can contain shadow and lighting passes (you can use surface shaders for shader replacement). This can be useful for doing rendering of special effects and scene debugging.

Shader replacement tags in built-in Unity shaders
-------------------------------------------------


All built-in Unity shaders have a "__RenderType__" tag set that can be used when rendering with replaced shaders. Tag values are the following:

* __Opaque__: most of the shaders ([Normal](shader-NormalFamily), [Self Illuminated](shader-SelfIllumFamily), [Reflective](shader-ReflectiveFamily), terrain shaders).
* __Transparent__: most semitransparent shaders ([Transparent](shader-TransparentFamily), Particle, Font, terrain additive pass shaders).
* __TransparentCutout__: masked transparency shaders ([Transparent Cutout](shader-TransparentCutoutFamily), two pass vegetation shaders).
* __Background__: Skybox shaders.
* __Overlay__: GUITexture, Halo, Flare shaders.
* __TreeOpaque__: terrain engine tree bark.
* __TreeTransparentCutout__: terrain engine tree leaves.
* __TreeBillboard__: terrain engine billboarded trees.
* __Grass__: terrain engine grass.
* __GrassBillboard__: terrain engine billboarded grass.


Built-in scene depth/normals texture
------------------------------------


A Camera has a built-in capability to render depth or depth+normals texture, if you need that in some of your effects. See [Camera Depth Texture](SL-CameraDepthTexture) page. Note that in some cases (depending on the hardware), the depth and depth+normals textures can internally be rendered using shader replacement. So it is important to have the correct "__RenderType__" tag in your shaders.

Code Example
------------

Your Start() function specifies the replacement shaders:

````
void Start() {
    camera.SetReplacementShader (EffectShader, "RenderType");
}
````
This requests that the EffectShader will use the RenderType key.  The EffectShader will have key-value tags for each RenderType that you want.  The Shader will look something like:

````
Shader "EffectShader" {
     SubShader {
         Tags { "RenderType"="Opaque" }
         Pass {
             ...
         }
     }
     SubShader {
         Tags { "RenderType"="SomethingElse" }
         Pass {
             ...
         }
     }
 ...
 }
````
SetReplacementShader will look through all the objects in the scene and, instead of using their normal shader, use the first subshader which has a matching value for the specified key.  In this example, any objects whose shader has Rendertype="Opaque" tag will be replaced by first subshader in EffectShader, any objects with RenderType="SomethingElse" shader will use second replacement subshader and so one.  Any objects whose shader does not have a matching tag value for the specified key in the replacement shader will not be rendered.





