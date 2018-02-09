# Shaders: ShaderLab and fixed function shaders


This tutorial teaches you the first steps of creating your own shaders, to help you control the look of your game and optimise the performance of the graphics.

Unity is equipped with a powerful shading and material language called
__ShaderLab__. In style it is similar to
CgFX and Direct3D Effects (.FX) languages - it describes everything
needed to display a [Material](class-Material).

Shaders describe properties that are exposed in Unity's
[Material Inspector](class-Material) and multiple shader
implementations (__SubShaders__) targeted
at different graphics hardware capabilities, each describing complete
graphics hardware rendering state, and vertex/fragment programs to use. Shader programs are written in the high-level [Cg/HLSL](SL-ShadingLanguage) programming language.

In this tutorial we'll describe how to write _very simple_ shaders using so-called "fixed function" notation. In the [next chapter](ShaderTut2) we'll introduce vertex and fragment [shader programs](SL-ShaderPrograms). We assume that the reader has a
basic understanding of [OpenGL](http://opengl.org/documentation/red_book) or Direct3D render
states, and has some knowledge of [HLSL](https://msdn.microsoft.com/en-us/library/bb509561.aspx), [Cg](http://http.developer.nvidia.com/Cg/Cg_language.html), [GLSL](http://www.opengl.org/documentation/glsl) or [Metal](https://developer.apple.com/library/ios/documentation/Metal/Reference/MetalShadingLanguageGuide/Introduction/Introduction.html) shader programming languages.


## Getting started

To create a new shader, either choose __Assets &gt; Create &gt; Shader &gt; Unlit Shader__ from the main menu, or duplicate an existing shader and work from that. The new shader can be edited by double-clicking it in the [Project View](ProjectView).

Unity has a way of writing _very simple_ shaders in so-called "fixed-function" notation. We'll start with this for simplicity. Internally
the fixed function shaders are converted to regular [vertex and fragment programs](SL-ShaderPrograms) at shader import time.

We'll start with a very basic shader:

```
Shader "Tutorial/Basic" {
    Properties {
        _Color ("Main Color", Color) = (1,0.5,0.5,1)
    }
    SubShader {
        Pass {
            Material {
                Diffuse [_Color]
            }
            Lighting On
        }
    }
}
```

This simple shader demonstrates one of the most basic shaders possible. It defines a color property called __Main Color__ and assigns it a default pink color (red=100% green=50% blue=50% alpha=100%). It then renders the object by invoking a __Pass__ and in that pass setting the diffuse material component to the property __\_Color__ and turning on per-vertex lighting.

To test this shader, create a new material, select the shader from the drop-down menu (__Tutorial-&gt;Basic__) and assign the Material to some object. Tweak the color in the Material Inspector and watch the changes. Time to move onto more complex things!

![](../uploads/SL/ShaderTutSimplestLit.png) 



## Basic vertex lighting


If you open an existing complex shader, it can be a bit hard to get a good overview. To get you started, we will dissect the built-in __VertexLit__ shader that ships with Unity. This shader uses fixed-function pipeline to do standard per-vertex lighting.




```
Shader "VertexLit" {
    Properties {
        _Color ("Main Color", Color) = (1,1,1,0.5)
        _SpecColor ("Spec Color", Color) = (1,1,1,1)
        _Emission ("Emmisive Color", Color) = (0,0,0,0)
        _Shininess ("Shininess", Range (0.01, 1)) = 0.7
        _MainTex ("Base (RGB)", 2D) = "white" { }
    }

    SubShader {
        Pass {
            Material {
                Diffuse [_Color]
                Ambient [_Color]
                Shininess [_Shininess]
                Specular [_SpecColor]
                Emission [_Emission]
            }
            Lighting On
            SeparateSpecular On
            SetTexture [_MainTex] {
                constantColor [_Color]
                Combine texture * primary DOUBLE, texture * constant
            }
        }
    }
}

```


All shaders start with the keyword [Shader](SL-Shader) followed by a string that represents the name of the shader. This is the name that is shown in the __Inspector__. All code for this shader must be put within the curly braces after it: __{ }__ (called a block).


* The name should be short and descriptive. It does not have to match the **.shader** file name.
* To put shaders in submenus in Unity, use slashes - e.g. __MyShaders/Test__ would be shown as __Test__ in a submenu called __MyShaders__, or __MyShaders-&gt;Test__.

The shader is composed of a __Properties__ block followed by __SubShader__ blocks. Each of these is described in sections below.


## Properties


At the beginning of the shader block you can define any properties that artists can edit in the [Material Inspector](class-Material). In the __VertexLit__ example the properties look like this:


![](../uploads/Main/ShaderTutProperties.png) 

The properties are listed on separate lines within the [Properties](SL-Properties) block. Each property starts with the internal name (__Color__, __MainTex__). After this in parentheses comes the name shown in the inspector and the type of the property. After that, the default value for this property is listed:


![](../uploads/Main/ShaderTutPropertyDetail.png) 

The list of possible types are in the [Properties Reference](SL-Properties). The default value depends on the property type. In the example of a color, the default value should be a four component vector.

We now have our properties defined, and are ready to start writing the actual shader.


## The shader body


Before we move on, let's define the basic structure of a shader file.

Different graphic hardware has different capabilities. For example, some graphics cards support fragment programs and others don't; some can lay down four textures per pass while the others can do only two or one; etc. To allow you to make full use of whatever hardware your user has, a shader can contain multiple __SubShaders__. When Unity renders a shader, it will go over all subshaders and use the first one that the hardware supports.




```
Shader "Structure Example" {
    Properties { /* ...shader properties... }
    SubShader {
    	// ...subshader that requires fancy DX11 / GLES3.1 hardware...
    }
    SubShader {
    	// ...subshader that requires DX9 SM3 / GLES3 hardware...
    }
    SubShader {
    	// ...subshader that might look ugly but runs on anything :)
    }
}

```

This system allows Unity to support all existing hardware and maximize the quality on each one. It does, however, result in some long shaders.

Inside each SubShader block you set the rendering state shared by all passes; and define rendering passes themselves. A complete list of available commands can be found in the [SubShader Reference](SL-SubShader).


## Passes


Each subshader is a collection of passes. For each pass, the object geometry is rendered, so there must be at least one pass. Our VertexLit shader has just one pass:



```
// ...snip...
Pass {
    Material {
        Diffuse [_Color]
        Ambient [_Color]
        Shininess [_Shininess]
        Specular [_SpecColor]
        Emission [_Emission]
    }
    Lighting On
    SeparateSpecular On
    SetTexture [_MainTex] {
        constantColor [_Color]
        Combine texture * primary DOUBLE, texture * constant
    }
}
// ...snip...

```

Any commands defined in a pass configures the graphics hardware to render the geometry in a specific way.

In the example above we have a __[Material](SL-Material)__ block that binds our property values to the fixed function lighting material settings. The command __Lighting On__ turns on the standard vertex lighting, and __SeparateSpecular On__ enables the use of a separate color for the specular highlight.

All of these command so far map very directly to the fixed function OpenGL/Direct3D hardware model. Consult [OpenGL red book](http://opengl.org/documentation/red_book) for more information on this.

The next command, __[SetTexture](SL-SetTexture)__, is very important. These commands define the textures we want to use and how to mix, combine and apply them in our rendering. __SetTexture__ command is followed by the property name of the texture we would like to use (__\_MainTex__ here) This is followed by a __combiner block__ that defines how the texture is applied. The commands in the combiner block are executed for each pixel that is rendered on screen.

Within this block we set a constant color value, namely the Color of the Material, __\_Color__. We'll use this constant color below.

In the next command we specify how to mix the texture with the color values. We do this with the __Combine__ command that specifies how to blend the texture with another one or with a color. Generally it looks like this:
    __Combine ColorPart, AlphaPart__

Here __ColorPart__ and __AlphaPart__ define blending of color (RGB) and alpha (A) components respectively. If __AlphaPart__ is omitted, then it uses the same blending as __ColorPart__.

In our VertexLit example:
    __Combine texture * primary DOUBLE, texture * constant__

Here __texture__ is the color coming from the current texture (here __\_MainTex__). It is multiplied (*) with the __primary__ vertex color. Primary color is the vertex lighting color, calculated from the Material values above. Finally, the result is multiplied by two to increase lighting intensity (__DOUBLE__). The alpha value (after the comma) is __texture__ multiplied by __constant__ value (set with __constantColor__ above). Another often used combiner mode is called __previous__ (not used in this shader). This is the result of any previous __SetTexture__ step, and can be used to combine several textures and/or colors with each other.


## Summary


Our VertexLit shader configures standard vertex lighting and sets up the texture combiners so that the rendered lighting intensity is doubled.

We could put more passes into the shader, they would get rendered one after the other. For now, though, that is not nessesary as we have the desired effect. We only need one SubShader as we make no use of any advanced features - this particular shader will work on any graphics card that Unity supports.

The VertexLit shader is one of the most basic shaders that we can think of. We did not use any hardware specific operations, nor did we utilize any of the more special and cool commands that ShaderLab and Cg/HLSL has to offer.

In the [next chapter](ShaderTut2) we'll proceed by explaining how to write custom vertex & fragment programs using Cg/HLSL language.
