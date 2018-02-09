#ShaderLab Syntax

All [Shaders](class-Shader) files in Unity are written in a declarative language called "ShaderLab". In the file, a nested-braces
syntax declares various things that describe the shader -- for example which shader properties should be shown in material inspector;
what kind of hardware fallbacks to do; what kind of blending modes to use etc.; and actual "shader code" is written in
`CGPROGRAM` snippets inside the same shader file (see [surface shaders](SL-SurfaceShaders) and [vertex and fragment shaders](SL-ShaderPrograms)).

This page and the child pages describes the nested-braces "ShaderLab" syntax. The `CGPROGRAM` snippets are written in regular
HLSL/Cg shading language, see [their documentation pages](SL-ShaderPrograms).


__Shader__ is the root command of a shader file. Each file must define one (and only one) Shader. It specifies how any objects whose material uses this shader are rendered.


##Syntax

````
Shader "name" { [Properties] Subshaders [Fallback] [CustomEditor] }
````

Defines a shader. It will appear in the material inspector listed under **name**. Shaders optionally can define a list of **properties** that show up in material inspector. After this comes a list of SubShaders, and optionally a fallback and/or a custom editor declaration.


##Details



###Properties

Shaders can have a list of [properties](SL-Properties). Any properties declared in a shader are shown in the [material inspector](class-Material) inside Unity. Typical properties are the object color, textures, or just arbitrary values to be used by the shader.


###SubShaders & Fallback

Each shader is comprised of a list of [sub-shaders](SL-SubShader). You must have at least one. When loading a shader, Unity will go through the list of subshaders, and pick the first one that is supported by the end user's machine. If no subshaders are supported, Unity will try to use [fallback shader](SL-Fallback).

Different graphic cards have different capabilities. This raises an eternal issue for game developers; you want your game to look great on the latest hardware, but don't want it to be available only to those 3% of the population. This is where subshaders come in. Create one subshader that has all the fancy graphic effects you can dream of, then add more subshaders for older cards. These subshaders may implement the effect you want in a slower way, or they may choose not to implement some details.

Shader "level of detail" (LOD) and "shader replacement" are two techniques that also build upon subshaders, see [Shader LOD](SL-ShaderLOD) and [Shader Replacemement](SL-ShaderReplacement) for details.


##Examples



Here is one of the simplest shaders possible:


````
// colored vertex lighting
Shader "Simple colored lighting"
{
    // a single color property
    Properties {
        _Color ("Main Color", Color) = (1,.5,.5,1)
    }
    // define one subshader
    SubShader
    {
        // a single pass in our subshader
        Pass
        {
            // use fixed function per-vertex lighting
            Material
            {
                Diffuse [_Color]
            }
            Lighting On
        }
    }
}
````

This shader defines a color property __\_Color__ (that shows up in material inspector as _Main Color_) with a default value of __(1,0.5,0.5,1)__. Then a single subshader is defined. The subshader consists of one [Pass](SL-Pass) that turns on fixed-function vertex lighting and sets up basic material for it.

See more complex examples at [Surface Shader Examples](SL-SurfaceShaderExamples) or
[Vertex and Fragment Shader Examples](SL-VertexFragmentShaderExamples).


## See Also

* [Properties Syntax](SL-Properties).
* [SubShader Syntax](SL-SubShader).
* [Pass Syntax](SL-Pass).
* [Fallback Syntax](SL-Fallback).
* [CustomEditor Syntax](SL-CustomEditor).
