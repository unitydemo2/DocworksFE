# Custom lighting models in Surface Shaders

When writing [Surface Shaders](SL-SurfaceShaders), you describe the properties of a surface (such as albedo color and normal), and a __Lighting Model__ computes the lighting interaction. 

There are two built-in lighting models: `Lambert` for diffuse lighting, and `BlinnPhong` for specular lighting. The _Lighting.cginc_ file inside Unity defines these models (Windows: _&lt;unity install path&gt;/Data/CGIncludes/Lighting.cginc_; macOS: _/Applications/Unity/Unity.app/Contents/CGIncludes/Lighting.cginc_).

Sometimes you might want to use a custom lighting model. You can do this with Surface Shaders. A lighting model is simply a couple of Cg/HLSL functions that match some conventions. 


## Declaring lighting models

A lighting model consists of regular functions with names that begin `Lighting`. You can declare them anywhere in your shader file, or one of the included files. The functions are:

1. `half4 Lighting<Name> (SurfaceOutput s, UnityGI gi);`
  Use this in forward rendering paths for light models that are _not_ dependent on the view direction.

1. `half4 Lighting<Name> (SurfaceOutput s, half3 viewDir, UnityGI gi);`
  Use this in forward rendering paths for light models that _are_ dependent on the view direction.

1. `half4 Lighting<Name>_Deferred (SurfaceOutput s, UnityGI gi, out half4 outDiffuseOcclusion, out half4 outSpecSmoothness, out half4 outNormal);`
  Use this in deferred lighting paths.

1. `half4 Lighting<Name>_PrePass (SurfaceOutput s, half4 light);`
  Use this in light prepass (legacy deferred) lighting paths.

Note that you don't need to declare all functions. A lighting model either uses view direction or it does not. Similarly, if the lighting model only works in forward rendering, do not declare the `_Deferred` or `_Prepass` function. This ensures that Shaders that use it only compile to forward rendering.

## Custom GI

Declare the following function to customize the decoding lightmap data and probes:

1. `half4 Lighting<Name>_GI (SurfaceOutput s, UnityGIInput data, inout UnityGI gi);`

Note that to decode standard Unity lightmaps and SH probes, you can use the built-in `DecodeLightmap` and `ShadeSHPerPixel` functions, as seen in `UnityGI_Base` in the _UnityGlobalIllumination.cginc_ file inside Unity (Windows: _&lt;unity install path&gt;/Data/CGIncludes/UnityGlobalIllumination.cginc_; macOS: _/Applications/Unity/Unity.app/Contents/CGIncludes/UnityGlobalIllumination.cginc__).

## Examples 
See documentation on [Surface Shader Lighting Examples](SL-SurfaceShaderLightingExamples) for more information.
