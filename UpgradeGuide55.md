#Upgrading to Unity 5.5




### Shaders: Physically Based Shading code changes

Physically based shading related code has been refactored in
Unity 5.5 (files `UnityStandardBRDF.cginc` and so on). In most
cases this does not affect your shader code directly, unless
you are manually calling some functions directly. Notable
changes are listed below.

- There are now functions to convert between smoothness,
  roughness and perceptual roughness:
  `PerceptualRoughnessToRoughness`,
  `RoughnessToPerceptualRoughness`, `SmoothnessToRoughness`,
  `RoughnessToSmoothness`.

- The visibility term in `UnityStandardBRDF.cginc` takes `roughness` and not `perceptualRoughness`.

- In older versions of Unity, it was possible to do a remapping with Marmoset roughness. With the move to GGX it no longer matches, and `UNITY_GLOSS_MATCHES_MARMOSET_TOOLBAG2` definition and associated code has been removed.

- All reads and writes into the Gbuffer should go through new functions `UnityStandardDataToGbuffer` / `UnityStandardDataFromGbuffer`.

- Your shader code should call `UnityGlossyEnvironmentSetup()` to initialize a `Unity_GlossyEnvironmentData` struct instead of doing it manually.

- The `roughness` variable of `Unity_GlossyEnvironmentData` is actually "perceptual roughness" but it hasn’t been renamed to avoid errors with existing shader code. Note: `UnityGlossyEnvironmentSetup` takes `smoothness` as a parameter and calculates perceptual roughness.

- The `ndotl` variable value in `UnityLight` is now calculated on the fly and any value written into the variable is ignored.

- The `UNITY_GI` macro is deprecated and should not be used anymore.


###Shaders: DirectX 9 half-pixel offset issue

Unity 5.5 now handles DX9 half-pixel offset rasterization in the background, which means you no longer need to fix DX9 half-pixel issues either in shaders or in code. See more details in [this blog post](http://aras-p.info/blog/2016/04/08/solving-dx9-half-pixel-offset/). If you use any of these checks in your code, they can now be removed:

- Checks in shaders for UNITY_HALF_TEXEL_OFFSET and shifting vertices/UVs based on that.
- Checks for D3D9 via SystemInfo.graphicsDeviceType or SystemInfo.graphicsDeviceVersion, and shifting vertices/UVs based on that.

The way Unity solves this now is by inserting half-pixel adjustment code into all vertex shaders that are being compiled. As a result, vertex shader constant register c255 becomes reserved by Unity, as well as two instructions being added to all shaders, and one more temporary register is used. This should not create problems, unless your vertex shaders use up all the available resources (constant/temporary registers and instruction slots) to the absolute maximum.


###Shaders: Z-buffer float inverted

The Z-buffer (depth buffer) direction has been inverted and this means the Z-buffer will now contain 1.0 at the near plane, 0.0 at the far plane. This, combined with the floating point depth buffer significantly increases the depth buffer precision resulting in less Z-fighting and better shadows, especially when using small near planes and large far planes.


Graphics API changes: 

- Clip space range is [near, 0] instead of [0, far]
- _CameraDepthTexture texture range is [1,0] instead of [0,1]
- Z-bias is negated before being applied 
- 24 bit depth buffers are switched to 32 bit float format


The following macros/functions will handle reversed Z situations without any other steps. If your shader was already using them, then no changes needed from your side:

- Linear01Depth(float z)
- LinearEyeDepth(float z)
- UNITY_CALC_FOG_FACTOR(coord)

However if you are fetching the Z buffer value manually you will need to do write code similar to:

```
float z = tex2D(_CameraDepthTexture, uv);
#if defined(UNITY_REVERSED_Z)
    z = 1.0f - z;
#endif
```

For clip space depth you can use the following macro. Please **note** that this macro will not alter clip space on OpenGL/ES plaforms but will remain `[-near, far]`:

```
float clipSpaceRange01 = UNITY_Z_0_FAR_FROM_CLIPSPACE(rawClipSpace);
```

**_ZBufferParams** now contains these values on platforms with a reversed depth buffer. See documentation on [platform-specific rendering differences](SL-PlatformDifferences) for more information.

```
x = -1+far/near
y = 1
z = x/far
w = 1/far
```

Z-bias is handled automatically by Unity but if you are using a native code rendering plugin you will need to negate it in your C/C++ code on matching platforms.


## Special Folder: Unity Editor subfolder named “Resources”


All subfolders of the folder named __"Editor"__ will be excluded from the build and will not load in Play mode in the Unity Editor.  Previously a subfolder named __"Resources"__ would have its assets included in the build.  These assets are still loadable by calling Resources.Load() in your Editor scripts.  

For example, these files are excluded from the build and will __not__ load when in Play mode in the Editor, but __will__ load if called from scripts:

- Editor/Foo/Resources/Bar.png *(this loads from Editor code as “Bar.png”)*
- Editor/Resources/Foo.png
- Editor/Resources/Editor/Resources/Foo.png *(this loads from Editor code as “Foo.png” but not as “Editor/Resources/Foo.png”)*

These assets will load in all situations:

- Resources/Editor/Foo.png
- Resources/Foo/Editor/Bar.png *(this loads as “Foo/Editor/Bar.png”)*
- Resources/Editor/Resources/Foo.png *(this loads as “Foo.png” and not as “Editor/Resources/Foo.png”)*


## Backface Tolerance and Final Gather

Previously the ‘Backface Tolerance’ parameter in [Lightmap Parameters](LightmapParameters) was not applied when using final gather for baked GI. It is now applied correctly. The parameter now affects both the realtime GI and baked GI stages (including the final gather).

Affected scenes are mainly ones with single sided geometry (like billboards) where it is important to be able to adjust the ‘Backface Tolerance’ in order to avoid invalidating texels that are seeing the backface of single sided geometry. In scenes that use billboards and final gather the lightmaps can now be improved by adjusting ‘Backface Tolerance’, however other scenes might also be affected, if a non-default ‘Backface Tolerance’ is applied, since it is now correctly accounted for in the final gather stage.


## Standard shader BRDF2 now uses GGX approximation

BRDF2, the standard shader type set on mobile platforms by default, now uses GGX approximation instead of Blinn-Phong. This makes it look closer to BRDF1 (used on desktops by default) and improves on visual quality. 

Should you need to preserve legacy approximation you should modify the BRDF2 code in UnityStandardBRDF.cginc which has the new implementation inside the #if UNITY_BRDF_GGX statement (this is also used by BRDF1 to pick GGX). Change the definition in UnityStandardConfig.cginc or change #if UNITY_BRDF_GGX  to #if 0 in the BRDF2_Unity_PBS function.

## Gradle for Android

You can now use [Gradle](android-gradle-overview) to build for Android.

Gradle is not as strict about errors compared with the existing Unity Android build system, meaning that some existing projects may be hard to convert to Gradle. See documentation on [Gradle troubleshooting](android-gradle-troubleshooting) to identify and solve these build failures. 


## Instantiate Object overload has changed

The specific overload of the Instantiate function that by default, takes a parameter for the original GameObject and one for a parent Transform has been changed to work differently. It no longer interprets the original GameObject's position and rotation as a world space position and rotation, thus ignoring the position and rotation of the specified parent Transform. 

It now interprets the position and rotation as a local position and rotation within the space of the specified parent Transform, by default. This is consistent with behavior in the Editor. Your scripts will not be automatically updated. This means when you run scripts containing calls to this overload of Instantiate that have not been updated to account for this change, you may experience unexpected behavior.


##Renderers and LOD Group components behavior

Disabling a LOD Group component no longer disables the Renderers attached to it. The LOD Group settings only apply to the Renderers when the LOD Group component is enabled. Unity automatically applies this change when you upgrade your project, and the change cannot be reverted.