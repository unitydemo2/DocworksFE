# Built-in shader include files


Unity contains several files that can be used by your [shader programs](SL-ShaderPrograms) to bring in predefined variables and helper functions. This is done by the standard `#include` directive, e.g.:

    CGPROGRAM
    // ...
    #include "UnityCG.cginc"
    // ...
    ENDCG

Shader include files in Unity are with `.cginc` extension, and the built-in ones are:

* `HLSLSupport.cginc` - _(automatically included)_ Helper macros and definitions for cross-platform shader compilation.
* `UnityShaderVariables.cginc` - _(automatically included)_ Commonly used global variables.
* `UnityCG.cginc` - commonly used [helper functions](SL-BuiltinFunctions).
* `AutoLight.cginc` - lighting & shadowing functionality, e.g. [surface shaders](SL-SurfaceShaders) use this file internally.
* `Lighting.cginc` - standard [surface shader](SL-SurfaceShaders) lighting models; automatically included when you're writing surface shaders.
* `TerrainEngine.cginc` - helper functions for Terrain & Vegetation shaders.

These files are found inside Unity application (__{unity install path}/Data/CGIncludes/UnityCG.cginc__ on Windows, __/Applications/Unity/Unity.app/Contents/CGIncludes/UnityCG.cginc__ on Mac), if you want to take a look at what exactly is done in any of the helper code.


## HLSLSupport.cginc


This file is automatically included when compiling CGPROGRAM shaders (but not included for HLSLPROGRAM ones). It declares various [preprocessor macros](SL-BuiltinMacros) to aid in multi-platform shader development.


## UnityShaderVariables.cginc

This file is automatically included when compiling CGPROGRAM shaders (but not included for HLSLPROGRAM ones). It declares various [built-in global variables](SL-UnityShaderVariables) that are commonly used in shaders.


## UnityCG.cginc


This file is often included in Unity shaders. It declares many [built-in helper functions](SL-BuiltinFunctions) and data structures.

#### Data structures in UnityCG.cginc


* struct `appdata_base`: vertex shader input with position, normal, one texture coordinate.
* struct `appdata_tan`: vertex shader input with position, normal, tangent, one texture coordinate.
* struct `appdata_full`: vertex shader input with position, normal, tangent, vertex color and two texture coordinates.
* struct `appdata_img`: vertex shader input with position and one texture coordinate.


