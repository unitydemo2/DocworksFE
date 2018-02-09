Custom Lighting models in Surface Shaders
=========================================


When writing [Surface Shaders](SL-SurfaceShaders), you're describing properties of a surface (albedo color, normal, ...) and the lighting interaction is computed by a __Lighting Model__. Built-in lighting models are __Lambert__ (diffuse lighting) and __BlinnPhong__ (specular lighting).

Sometimes you might want to use a custom lighting model, and it is possible to do that in Surface Shaders. Lighting model is nothing more than a couple of Cg/HLSL functions that match some conventions. The built-in `Lambert` and `BlinnPhong` models are defined in `Lighting.cginc` file inside Unity (__{unity install path}/Data/CGIncludes/Lighting.cginc__ on Windows, __/Applications/Unity/Unity.app/Contents/CGIncludes/Lighting.cginc__ on Mac).


Lighting Model declaration
--------------------------


Lighting model is a couple of regular functions with names starting with `Lighting`. They can be declared anywhere in your shader file or one of included files. The functions are:

1. `half4 Lighting<Name> (SurfaceOutput s, UnityGI gi);`
  This is used in forward rendering path for light models that _are not_ view direction dependent (e.g. diffuse).

1. `half4 Lighting<Name> (SurfaceOutput s, half3 viewDir, UnityGI gi);`
  This is used in forward rendering path for light models that are view direction dependent.

1. `half4 Lighting<Name>_Deferred (SurfaceOutput s, UnityGI gi, out half4 outDiffuseOcclusion, out half4 outSpecSmoothness, out half4 outNormal);`
  This is used in deferred lighting path.

1. `half4 Lighting<Name>_PrePass (SurfaceOutput s, half4 light);`
  This is used in light prepass (legacy deferred) lighting path.

Note that you don't need to declare all functions. A lighting model either uses view direction or it does not. Similarly, if the lighting model only works in forward, do not declare the `_Deferred` or `_Prepass` function. This way, all Shaders that use it compile to forward rendering only.

Custom GI
---------


Similarly, customize the decoding lightmap data and probes by declaring the function below. 

1. `half4 Lighting<Name>_GI (SurfaceOutput s, UnityGIInput data, inout UnityGI gi);`

Note that to decode standard Unity lightmaps and SH probes, you can use the built-in __DecodeLightmap__ and __ShadeSHPerPixel__ functions, as seen in __UnityGI_Base__ in the `UnityGlobalIllumination.cginc` file inside Unity (__{unity install path}/Data/CGIncludes/UnityGlobalIllumination.cginc__ on Windows, __/Applications/Unity/Unity.app/Contents/CGIncludes/UnityGlobalIllumination.cginc__ on Mac).


Examples
--------


**[Surface Shader Lighting Examples](SL-SurfaceShaderLightingExamples)**
