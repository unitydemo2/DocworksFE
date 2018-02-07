# Shader assets

Shaders are assets that contain code and instructions for the graphics card to execute.
[Materials](class-Material) reference shaders, and setup their parameters (textures, colors and so on).

Unity contains some built-in shaders that are always available in your project (for example,
the [Standard shader](shader-StandardShader)). You can also [write your own shaders](ShadersOverview) and apply [post-processing effects](PostProcessingOverview).


## Creating a new shader

To create a new Shader, use __Assets__ &gt; __Create__ &gt; __Shader__ from the
main menu or the __Project View__ context menu. A shader is a text file
similar to a C# script, and is written in a combination of Cg/HLSL and ShaderLab languages
(see [writing shaders](ShadersOverview) page for details).

![Shader inspector.](../uploads/Shaders/Inspector-Shader.png)


### Shader import settings

This inspector section allows specifying default textures for a shader. Whenever a new
[Material](class-Material) is created with this shader, these textures are
automatically assigned.


### Shader Inspector

The Shader Inspector displays basic information about the shader (mostly [shader tags](SL-SubShaderTags)),
and allows compiling and inspecting low-level compiled code.

For [Surface Shaders](SL-SurfaceShaders), the __Show generated code__
button displays all the code that Unity generates to handle lighting and shadowing. If you really want
to customize the generated code, you can just copy and paste all of it back to your original shader file
and start tweaking.


![Shader compilation popup menu.](../uploads/Shaders/Inspector-ShaderCompilePopup.png)

The pop-up menu of the __Compile and show code__ button allows inspecting final
compiled shader code (e.g. assembly on Direct3D9, or low-level optimized GLSL for OpenGL ES) for selected
platforms. This is mostly useful while optimizing shaders for performance; often you do want to know how
many low-level instructions here generated in the end.

The low-level generated code is useful for pasting into GPU shader performance analysis tools (like
[AMD GPU ShaderAnalyzer](http://developer.amd.com/tools-and-sdks/graphics-development/gpu-shaderanalyzer/)
or [PVRShaderEditor](http://community.imgtec.com/developers/powervr/tools/pvrshadereditor/)).


## Shader compilation details

On shader import time, Unity does not compile the whole shader. This is because majority of shaders
have a lot of [variants](SL-MultipleProgramVariants) inside, and compiling all of them, for all possible
platforms, would take a very long time. Instead, this is done:

* At import time, only do minimal processing of the shader (surface shader generation etc.).
* Actually compile the shader variants only when needed.
* Instead of typical work of compiling 100-10000 internal shaders at import time, this usually ends up compiling just a handful.

At player build time, all the "not yet compiled" shader variants are compiled, so that they are in the game data even if the editor did not happen to use them.

However, this does mean that a shader might have an error in there, which is not detected at shader
import time. For example, you're running editor using Direct3D 11, but a shader has an error if compiled
for OpenGL. Or some [variants](SL-MultipleProgramVariants) of the shader does not fit into shader model 2.0
instruction limits, etc. These errors will be shown in the inspector if editor needs them; but it's also a
good practice to manually fully compile the shader for platforms you need, to check for errors. This can be
done using the __Compile and show code__ pop-up menu in the shader inspector.

Shader compilation is carried out using a background process named `UnityShaderCompiler` that is started by Unity
whenever it needs to compile shaders. Multiple compiler processes can be started (generally one per CPU
core in your machine), so that at player build time shader compilation can be done in parallel. While the
editor is not compiling shaders, the compiler processes do nothing and do not consume computer resources,
so there's no need to worry about them. They are also shut down when Unity editor quits.

Individual shader variant compilation results are cached in the project, under `Library/ShaderCache` folder.
This means that 100% identical shaders or their snippets will reuse previously compiled results. It also
means that the shader cache folder can become quite large, if you have a lot of shaders that are changed
often. It is always safe to delete it; it will just cause shader variants to be recompiled.



## Further reading

* [Material](class-Material) assets.
* [Writing Shaders overview](ShadersOverview).
* [Shader reference](SL-Reference).

