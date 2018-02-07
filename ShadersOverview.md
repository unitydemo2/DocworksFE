#Writing Shaders

Shaders in Unity can be written in one of three different ways:

###Surface Shaders

[Surface Shaders](SL-SurfaceShaders) are your best option if your Shader needs to be affected by lights and shadows. Surface Shaders make it easy to write complex Shaders in a compact way - it's a higher level of abstraction for interaction with Unity's lighting pipeline. Most Surface Shaders automatically support both forward and deferred lighting. You write Surface Shaders in a couple of lines of **Cg/HLSL**, and a lot more code gets auto-generated from that.

Do not use Surface Shaders if your Shader is not doing anything with lights. For [post-processed effects](PostProcessingOverview) or many special-effect Shaders, Surface Shaders are a suboptimal option, since they do a bunch of lighting calculations for no good reason.


###Vertex and Fragment Shaders

[Vertex and Fragment Shaders](SL-ShaderPrograms) are required if your Shader doesn't need to interact with lighting, or if you need some very exotic effects that the Surface Shaders can't handle. Shader programs written this way are the most flexible way to create the effect you need (even Surface Shaders are automatically converted to a bunch of Vertex and Fragment Shaders), but that comes at a price: you have to write more code and it's harder to make it interact with lighting. These Shaders are written in **Cg/HLSL** as well.


###Fixed Function Shaders

Fixed Function Shaders are legacy Shader syntax for very simple effects. It is advisable to write programmable Shaders, since that allows much more flexibility. Fixed function shaders are entirely written in a language called **ShaderLab**, which is similar to Microsoft's .FX files or NVIDIA's CgFX. Internally, all Fixed Function Shaders are converted into [Vertex and Fragment Shaders](SL-ShaderPrograms) at shader import time.


##ShaderLab

Regardless of which type you choose, the actual Shader code is always wrapped in ShaderLab, which is used to organize the Shader structure. It looks like this:

````
Shader "MyShader" {
    Properties {
        _MyTexture ("My Texture", 2D) = "white" { }
        // Place other properties like colors or vectors here as well
    }
    SubShader {
        // here goes your
        // - Surface Shader or
        // - Vertex and Fragment Shader or
        // - Fixed Function Shader
    }
    SubShader {
        // Place a simpler "fallback" version of the SubShader above
        // that can run on older graphics cards here
    }
}
````

We recommend that you start by reading about some basic concepts of the ShaderLab syntax in the [ShaderLab reference](SL-Shader) and then move on to the tutorials listed below.

The tutorials include plenty of examples for the different types of Shaders. Unity's [post-processing effects](PostProcessingOverview) allows you to create many interesting effects with shaders.

Read on for an introduction to shaders, and check out the [Shader reference](SL-Reference)!


* [Tutorial: ShaderLab & Fixed Function Shaders](ShaderTut1)
* [Tutorial: Vertex and Fragment Shaders](ShaderTut2)
* [Surface Shaders](SL-SurfaceShaders)
* [Writing Vertex and Fragment Shaders](SL-ShaderPrograms)
