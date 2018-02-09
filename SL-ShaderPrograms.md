Writing vertex and fragment shaders
===================================


__ShaderLab__ shaders encompass more than just "hardware shaders". They do many things. They describe properties that are displayed in the Material Inspector, contain multiple shader implementations for different graphics hardware, configure fixed function hardware state and so on. The actual programmable shaders - like vertex and fragment programs - are just a part of the whole ShaderLab's "shader" concept. Take a look at [shader tutorial](ShaderTut2) for a basic introduction. Here we'll call the low-level hardware shaders __shader programs__.

**If you want to write shaders that interact with lighting, take a look at [Surface Shaders](SL-SurfaceShaders) documentation**. For some examples, take a look at [__Vertex and Fragment Shader Examples__](SL-VertexFragmentShaderExamples). The rest of this page will assume shaders that do not interact with Unity lights (e.g. special effects, [Image Effects](comp-ImageEffects) etc.)

Shader programs are written in [HLSL language](SL-ShadingLanguage), by embedding "snippets" in the shader text, somewhere inside the [Pass](SL-Pass) command. They usually look like this:

````
  Pass {
      // ... the usual pass state setup ...
      
      CGPROGRAM
      // compilation directives for this snippet, e.g.:
      #pragma vertex vert
      #pragma fragment frag
      
      // the Cg/HLSL code itself
      
      ENDCG
      // ... the rest of pass setup ...
  }
````


## HLSL snippets


HLSL program snippets are written between __CGPROGRAM__ and __ENDCG__ keywords, or alternatively between __HLSPROGRAM__ and __ENDHLSL__. The latter form does *not* automatically include HLSLSupport and UnityShaderVariables [built-in header files](SL-BuiltinIncludes).

At the start of the snippet compilation directives can be given as __#pragma__ statements. Directives indicating which shader functions to compile:

* __#pragma vertex__ _name_ - compile function _name_ as the vertex shader.
* __#pragma fragment__ _name_ - compile function _name_ as the fragment shader.
* __#pragma geometry__ _name_ - compile function _name_ as DX10 geometry shader. Having this option automatically turns on __#pragma target 4.0__, described below.
* __#pragma hull__ _name_ - compile function _name_ as DX11 hull shader. Having this option automatically turns on __#pragma target 5.0__, described below.
* __#pragma domain__ _name_ - compile function _name_ as DX11 domain shader. Having this option automatically turns on __#pragma target 5.0__, described below.

Other compilation directives:

* __#pragma target__ _name_ - which shader target to compile to. See [Shader Compilation Targets](SL-ShaderCompileTargets) page for details.
* __#pragma only_renderers__ _space separated names_ - compile shader only for given renderers. By default shaders are compiled for all renderers. See _Renderers_ below for details.
* __#pragma exclude_renderers__ _space separated names_ - do not compile shader for given renderers. By default shaders are compiled for all renderers. See _Renderers_ below for details.
* __#pragma multi_compile ...__  - for working with [multiple shader variants](SL-MultipleProgramVariants).
* __#pragma enable_d3d11_debug_symbols__ - generate debug information for shaders compiled for DirectX 11, this will allow you to debug shaders via Visual Studio 2012 (or higher) Graphics debugger.
* __#pragma hardware_tier_variants__ _renderer name_ - generate [multiple shader hardware variants](SL-MultipleProgramVariants) of each compiled shader, for each hardware tier that could run the selected renderer. See _Renderers_ below for details.

Each snippet must contain at least a vertex program and a fragment program. Thus __#pragma vertex__ and __#pragma fragment__ directives are required.


Compilation directives that don't do anything starting with Unity 5.0 and can be safely removed: `#pragma glsl`, `#pragma glsl_no_auto_normalization`, `#pragma profileoption`, `#pragma fragmentoption`.



## Rendering platforms


Unity supports several rendering APIs (e.g. Direct3D 9 and OpenGL), and by default all shader programs are compiled into all supported renderers. You can indicate which renderers to compile to using __#pragma only_renderers__ or __#pragma exclude_renderers__ directives. This is mostly useful in cases where you are explicitly using some shader language features that you know aren't possible on some platforms. Supported renderer names are:

* __d3d9__ - Direct3D 9
* __d3d11__ - Direct3D 11/12
* __glcore__ - OpenGL 3.x/4.x
* __gles__ - OpenGL ES 2.0
* __gles3__ - OpenGL ES 3.x
* __metal__ - iOS/Mac Metal
* __vulkan__ - Vulkan
* __d3d11_9x__ - Direct3D 11 9.x feature level, as commonly used on WSA platforms
* __xboxone__ - Xbox One
* __ps4__ - PlayStation 4
* __psp2__ - PlayStation Vita
* __n3ds__ - Nintendo 3DS
* __wiiu__ - Nintendo Wii U


For example, this line would only compile shader into D3D9 mode:

	#pragma only_renderers d3d9


## See Also

* [Accessing Material Properties](SL-PropertiesInPrograms).
* [Writing Multiple Shader Program Variants](SL-MultipleProgramVariants).
* [Shader Compilation Targets](SL-ShaderCompileTargets).
* [Shading Language Details](SL-ShadingLanguage).
* [Shader Preprocessor Macros](SL-BuiltinMacros).
* [Platform Specific Rendering Differences](SL-PlatformDifferences).
