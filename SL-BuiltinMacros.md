# Predefined Shader preprocessor macros


Unity defines several preprocessor macros when compiling [Shader programs](SL-ShaderPrograms).

## Target platform

|__Macro:__|__Target platform:__|
|:---|:---|
|`SHADER_API_D3D11` | Direct3D 11 |
|`SHADER_API_GLCORE` | Desktop OpenGL "core" (GL 3/4) |
|`SHADER_API_GLES` | OpenGL ES 2.0 |
|`SHADER_API_GLES3` | OpenGL ES 3.0/3.1 |
|`SHADER_API_METAL` | iOS/Mac Metal |
|`SHADER_API_VULKAN` | Vulkan |
|`SHADER_API_D3D11_9X` | Direct3D 11 "feature level 9.x" target for Universal Windows Platform |
|`SHADER_API_PS4` | PlayStation 4. `SHADER_API_PSSL` is also defined. |
|`SHADER_API_XBOXONE` | Xbox One |
|`SHADER_API_PSP2` | PlayStation Vita |
|`SHADER_API_WIIU` | Nintendo Wii U |


`SHADER_API_MOBILE` is defined for all general mobile platforms (GLES, GLES3, METAL, PSP2).

Additionally, `SHADER_TARGET_GLSL` is defined when the target shading language is GLSL (always true for OpenGL/GLES platforms).


## Shader target model 

`SHADER_TARGET` is defined to a numeric value that matches the Shader target compilation model (that is, matching `#pragma target` directive). For example, `SHADER_TARGET` is `30` when compiling into Shader model 3.0. You can use it in Shader code to do conditional checks. For example:

````
#if SHADER_TARGET < 30
    // less than Shader model 3.0:
    // very limited Shader capabilities, do some approximation
#else
    // decent capabilities, do a better thing
#endif
````


## Unity version

`UNITY_VERSION` contains the numeric value of the Unity version. For example, `UNITY_VERSION` is `501` for Unity 5.0.1. This can be used for version comparisons if you need to write Shaders that use different built-in Shader functionality. For example, a `#if UNITY_VERSION >= 500` preprocessor check only passes on versions 5.0.0 or later.


## Shader stage being compiled

Preprocessor macros `SHADER_STAGE_VERTEX`, `SHADER_STAGE_FRAGMENT`, `SHADER_STAGE_DOMAIN`, `SHADER_STAGE_HULL`, `SHADER_STAGE_GEOMETRY`, `SHADER_STAGE_COMPUTE` are defined when compiling each Shader stage. Typically they are useful when sharing Shader code between pixel Shaders and compute Shaders, to handle cases where some things have to be done slightly differently.


## Platform difference helpers

Direct use of these platform macros is discouraged, as they don't always contribute to the future-proofing of your code. For example, if you're writing a Shader that checks for D3D11, you may want to ensure that, in the future, the check is extended to include Vulkan. Instead, Unity defines several helper macros (in [`HLSLSupport.cginc`](SL-BuiltinIncludes)):

|__Macro:__|__Use:__|
|:---|:---|
|`UNITY_BRANCH` | Add this before conditional statements to tell the compiler that this should be compiled into an actual branch. Expands to `[branch]` when on HLSL platforms. |
|`UNITY_FLATTEN` | Add this before conditional statements to tell the compiler that this should be flattened to avoid an actual branch instruction. Expands to `[flatten]` when on HLSL platforms. |
|`UNITY_NO_SCREENSPACE_SHADOWS` | Defined on platforms that do not use cascaded screenspace shadowmaps (mobile platforms). |
|`UNITY_NO_LINEAR_COLORSPACE` | Defined on platforms that do not support Linear color space (mobile platforms). |
|`UNITY_NO_RGBM` | Defined on platforms where RGBM compression for lightmaps is not used (mobile platforms). |
|`UNITY_NO_DXT5nm` | Defined on platforms that do not use DXT5nm normal-map compression (mobile platforms). |
|`UNITY_FRAMEBUFFER_FETCH_AVAILABLE` | Defined on platforms where "framebuffer color fetch" functionality can be available (generally iOS platforms - OpenGL ES 2.0, 3.0 and Metal). |
|`UNITY_USE_RGBA_FOR_POINT_SHADOWS` | Defined on platforms where point light shadowmaps use RGBA Textures with encoded depth (other platforms use single-channel floating point Textures). |
|`UNITY_ATTEN_CHANNEL` | Defines which channel of light attenuation Texture contains the data; used in per-pixel lighting code. Defined to either 'r' or 'a'. |
|`UNITY_HALF_TEXEL_OFFSET` | Defined on platforms that need a half-texel offset adjustment in mapping texels to pixels (e.g. Direct3D 9). |
|`UNITY_UV_STARTS_AT_TOP` | Always defined with value of 1 or 0. A value of 1 is on platforms where Texture V coordinate is 0 at the "top" of the Texture. Direct3D-like platforms use value of 1; OpenGL-like platforms use value of 0. |
|`UNITY_MIGHT_NOT_HAVE_DEPTH_Texture` | Defined if a platform might emulate shadow maps or depth Textures by manually rendering depth into a Texture. |
|`UNITY_PROJ_COORD(a)` | Given a 4-component vector, this returns a Texture coordinate suitable for projected Texture reads. On most platforms this returns the given value directly. |
|`UNITY_NEAR_CLIP_VALUE` | Defined to the value of near clipping plane. Direct3D-like platforms use 0.0 while OpenGL-like platforms use -1.0. |
|`UNITY_VPOS_TYPE` | Defines the data type required for pixel position input (VPOS): `float2` on D3D9, `float4` elsewhere. |
|`UNITY_CAN_COMPILE_TESSELLATION` | Defined when the Shader compiler "understands" the tessellation Shader HLSL syntax (currently only D3D11). |
|`UNITY_INITIALIZE_OUTPUT(type,name)` | Initializes the variable _name_ of given _type_ to zero. |
|`UNITY_COMPILER_HLSL`, `UNITY_COMPILER_HLSL2GLSL`, `UNITY_COMPILER_CG` | Indicates which Shader compiler is being used to compile Shaders - respectively: Microsoft's HLSL, HLSL to GLSL translator, and NVIDIA's Cg. See documentation on [Shading Languages](SL-ShadingLanguage) for more details. Use this if you run into very specific Shader syntax handling differences between the compilers, and want to write different code for each compiler. |

* `UNITY_REVERSED_Z` - defined on plaftorms using reverse Z buffer. Stored Z values are in the range 1..0 instead of 0..1.


## Shadow mapping macros


Declaring and sampling shadow maps can be very different depending on the platform. Unity has several macros to help with this:

|__Macro:__ |__Use:__ |
|:---|:---|
| `UNITY_DECLARE_SHADOWMAP(tex)` | Declares a shadowmap Texture variable with name "tex".|
| `UNITY_SAMPLE_SHADOW(tex,uv)` | Samples shadowmap Texture "tex" at given "uv" coordinate (XY components are Texture location, Z component is depth to compare with). Returns single float value with the shadow term in 0..1 range.|
| ` UNITY_SAMPLE_SHADOW_PROJ(tex,uv)` | Similar to above, but does a projective shadowmap read. "uv" is a float4, all other components are divided by .w for doing the lookup.|

__NOTE:__ Not all graphics cards support shadowmaps. Use [SystemInfo.SupportsRenderTextureFormat](ScriptRef:SystemInfo.SupportsRenderTextureFormat) to check for support.

## Constant buffer macros


Direct3D 11 groups all Shader variables into "constant buffers". Most of Unity's built-in variables are already grouped, but for variables in your own Shaders it might be more optimal to put them into separate constant buffers depending on expected frequency of updates.

Use `CBUFFER_START(name)` and `CBUFFER_END` macros for that:

````
CBUFFER_START(MyRarelyUpdatedVariables)
    float4 _SomeGlobalValue;
CBUFFER_END
````


## Texture/Sampler declaration macros

Usually you would use `texture2D` in Shader code to declare a Texture and Sampler pair.
However on some platforms (such as DX11), Textures and Samplers are separate GameObjects,
and maximum possible Sampler count is quite limited. Unity has some macros to declare
Textures without Samplers, and to sample a Texture using a Sampler from another Texture.
Use this if you end up running into Sampler limits, and you know that several of your
Textures can in fact share a Sampler (Samplers define Texture filtering and wrapping modes).

|__Macro:__ |__Use:__ |
|:---|:---|
|`UNITY_DECLARE_TEX2D(name)` | Declares a Texture and Sampler pair. |
|`UNITY_DECLARE_TEX2D_NOSAMPLER(name)` | Declares a Texture without a Sampler. |
|`UNITY_DECLARE_TEX2DARRAY(name)` | Declares a Texture array Sampler variable. |
|`UNITY_SAMPLE_TEX2D(name,uv)` | Sample from a Texture and Sampler pair, using given Texture coordinate. |
|`UNITY_SAMPLE_TEX2D_SAMPLER( name,samplername,uv)` | Sample from Texture (name), using a Sampler from another Texture (samplername). |
|`UNITY_SAMPLE_TEX2DARRAY(name,uv)` | Sample from a Texture array with a float3 UV; the z component of the coordinate is array element index. |
|`UNITY_SAMPLE_TEX2DARRAY_LOD(name,uv,lod)`| Sample from a Texture array with an explicit mipmap level.|

For more information, see documentation on [Sampler States](SL-SamplerStates).


## Surface Shader pass indicators


When [Surface Shaders](SL-SurfaceShaders) are compiled, they generate a lot of code for various passes to do lighting. When compiling each pass, one of the following macros is defined:

|__Macro:__ |__Use:__ |
|:---|:---|
| `UNITY_PASS_FORWARDBASE` | Forward rendering base pass (main directional light, lightmaps, SH). |
| `UNITY_PASS_FORWARDADD` | Forward rendering additive pass (one light per pass). |
| `UNITY_PASS_DEFERRED` | Deferred shading pass (renders g buffer). |
| `UNITY_PASS_SHADOWCASTER` | Shadow caster and depth Texture rendering pass. |
| `UNITY_PASS_PREPASSBASE` | Legacy deferred lighting base pass (renders normals and specular exponent). |
| `UNITY_PASS_PREPASSFINAL` | Legacy deferred lighting final pass (applies lighting and Textures). |

## Disable Auto-Upgrade

`UNITY_SHADER_NO_UPGRADE` allows you to disable Unity from automatically upgrading or modifying your shader file.


## See also

* [Built-in Shader include files](SL-BuiltinIncludes)
* [Built-in Shader variables](SL-UnityShaderVariables)
* [Vertex and Fragment program examples](SL-VertexFragmentShaderExamples)

---

<span class="page-edit">• 2017-05-16  <!-- include IncludeTextAmendPageNoEdit --></span><br/>
