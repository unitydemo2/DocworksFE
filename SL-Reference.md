# Shader Reference


Shaders in Unity can be written in one of three different ways:


* as **[surface shaders](SL-SurfaceShaders)**,
* as **[vertex and fragment shaders](SL-ShaderPrograms)** or
* as **fixed function shaders**.

The [shader tutorial](Shaders) can guide you on choosing the right type for your needs.

Regardless of which type you choose, the actual meat of the shader code will always be wrapped in a language called ShaderLab, which is used to organize the shader structure. It looks like this:



````
Shader "MyShader" {
    Properties {
        _MyTexture ("My Texture", 2D) = "white" { }
        // other properties like colors or vectors go here as well
    }
    SubShader {
        // here goes the 'meat' of your
        // - surface shader or
        // - vertex and program shader or
        // - fixed function shader
    }
    SubShader {
        // here goes a simpler version of the SubShader
        // above than can run on older graphics cards
    }
}
````

We recommend that you start by reading about some basic concepts of the [ShaderLab syntax](SL-Shader) in the sections listed below and then to move on to read about surface shaders or vertex and fragment shaders in other sections. Since fixed function shaders are written using ShaderLab only, you will find more information about them in the ShaderLab reference itself.

The reference below includes plenty of examples for the different types of shaders. For even more examples of surface shaders in particular, you can get the source of Unity's built-in shaders from the [Resources section](http://www.unity3d.com/support/resources/assets/built-in-shaders). Unity's [post-processing effects](PostProcessingOverview) allows you to create many interesting effects with shaders.

Read on for shader reference, and check out the [shader tutorial](Shaders) as well!


## See Also

* [Writing Surface Shaders](SL-SurfaceShaders).
* [Writing vertex and fragment shaders](SL-ShaderPrograms).
* [ShaderLab Syntax Reference](SL-Shader).
* [Shader Assets](class-Shader).
* [Advanced ShaderLab Topics](SL-AdvancedTopics).
