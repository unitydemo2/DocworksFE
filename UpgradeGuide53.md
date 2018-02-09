Upgrading to Unity 5.3
=================

Global Illumination
-------------------

Lightmap Snapshot was renamed to Lighting Data asset. The internal format of the lighting data was changed after the upgrade to Enlighten 3. Snapshots from a previous versions of Unity are no longer supported and should be rebaked.

This also affects streamed scene AssetBundles with realtime GI. Lightmap data won’t be loaded and thus such bundles should be also rebuilt.

Light probes and environment lighting is now consistent in gamma and linear color space. Some differences in environment lighting compared to Unity 5.2 is to be expected. Output is matching Unity 4.x intensity wise now but since 4.x and our light projection code generates L2 coefficients and Enlighten only outputs L1, the falloff for the final light probes can appear different. L2 support for light probes will appear in a future release. Directional non-important lights should now match 4.x.
Light probes are always passed to the shaders in linear color space and final gamma conversion happens on the GPU. If you are using Unity's ShadeSHxxx functions for evaluating the spherical harmonics in the shader, you should not have to change your shaders. In UNITY_STANDARD_SIMPLE shaders the SH evaluation is not split between the pixel and vertex shader, so we limit the linear to gamma conversions to only happen once and only in the vertex shader. On more advanced GPUs the calculation is split between vertex and fragment shader.


Shuriken
--------

The particle size in the Collision Module has been replaced by a new parameter: Radius Scale. This new parameter acts as a multiplier on the actual particle size. If you were using the old value to do anything other than approximate the particle sizes, then you will need to reconfigure your collision bounds using the new parameter.

Multi Scene Editing
-------------------

The multi scene editing feature introduces new API through EditorSceneManager and SceneManager. Which means that many of the API's on EditorApplication and Application has been deprecated.

* EditorApplication.NewScene
* EditorApplication.NewEmptyScene
* EditorApplication.OpenScene
* EditorApplication.OpenSceneAdditive
* EditorApplication.SaveScene
* EditorApplication.SaveCurrentSceneIfUserWantsTo
* EditorApplication.SaveCurrentSceneIfUserWantsToForce

The above all have equivalent APIs on EditorSceneManager

* EditorApplication.currentScene

Internally this will return the name of the active scene in the Scene Manager, but to get all currently open scenes use the EditorSceneManager APIs

* EditorApplication.MarkSceneDirty
* EditorApplication.isSceneDirty

Each scene now has its own dirty flag. Get the scenes through the EditorSceneManager and check their state. Setting scenes dirty is also done through the EditorSceneManager. The deprecated APIs all operate on the active scene only.

* Application.LoadLevel
* Application.LoadLevelAsync
* Application.LoadLevelAdditive
* Application.LoadLevelAdditiveAsync

Application.LoadLevel\[Async\]\(path\) redirects to SceneManager.LoadScene\[Async\](path, false) and Application.LoadLevelAdditive\[Async\]\(path\) redirects to SceneManager.LoadScene\[Async\](path, true) 

* Application.loadedLevel
* Application.loadedLevelName

These respectively gets the Build Setting Index of the active scene and the name of the active scene. You should use the SceneManager to get the indices and names of all loaded scene.

Note also that EditorApplication.OpenSceneAdditive can nolonger be called during play in the Editor. That also means it cannot be called from a [PostprocessScene] callback. If EditorApplication.OpenSceneAdditive is called during play anyway, then play mode will be stopped.

Precompiled Shader Assets
-------------------------

Precompiled shader assets are no longer supported - this means you can no longer click "show compiled code" and copy the resulting disassembly into a new shader asset. Old shader assets that are precompiled will be marked as unsupported.

The "show compiled code" in the shader inspector will still work and will display the disassembly of the shader on each platform.

Likewise you can still view the generated code for a surface shader, modify it, and copy that into a new shader asset - since it is only the HLSL source you are modifying.

This will affect AssetBundles built in previous versions of Unity - they have compiled shader assets inside them by definition. Any shaders in such bundles will need to be rebuilt.

For more detailed information you can see this [unity blog post about upcoming feature deprecation](http://blogs.unity3d.com/2015/08/27/plans-for-graphics-features-deprecation/).

OpenGL 4.x support on desktop
-----------------------------

As a new feature, the OS X Editor and Standalone now support the new GL backend, which enables the use of OpenGL 3.x and 4.x features such as tessellation and geometry shaders. However, as Apple restricts the OpenGL version on OS X desktop to 4.1 at most, it does not support all DirectX 11 features (such as Unordered Access Views or Compute Shaders). This means that all shaders that are configured to target Shader Level 5.0 (with #pragma target 50) will fail to load on OS X.

Therefore a new shader target level is introduced: #pragma target gl4.1. This target level requires at least OpenGL 4.1 or DirectX 11.0 Shader Level 5 on desktop, or OpenGL ES 3.1 + Android Extension Pack on mobiles.

AssetBundles
------------
AssetBundle’s container format was changed in order to support new LZ4 compression and have a basis for further improvements. Bundles created in earlier version (2.x, 3.x) are deprecated and not supported.
Bundles created in Unity 4.x, 5.0-5.2 are supported and could be loaded. But, if they were already cached on a user device using WWW.LoadFromCacheOrDownload method, they will be redownloaded. Also take in mind that data in such bundles might be a subject to change (see e.g. Global Illumination section).

GetComponent(s)InChildren
------------
GetComponentsInChildren has a slightly changed behaviour in the case where you invoke it on a gameObject who has a parent that is inactive. Previously you would always get an empty array as a result. Because that is never what you want, and because that meant GetComponentsOnChildren didn't work on prefabs, this has been changed to ignore any active state from the target game object's parents. Also, the singular version GetComponentInChildren() now has an optional includeInactive argument.

UI/default shaders
------------

Using a default new UI shader on non new UI objects is not longer supported by default. Previously there was an 'if' check to determine whether or not the _clipRect should be used but for performance reasons this check was removed. To continue using a new UI shader on a non new UI object you will need to specify a valid clipRect yourself.

Point and spot shadow casting lights
------------

Point lights that are selected to cast shadows now have a working Bias slider, to allow adjustment and balancing of shadowing artifacts (under shadowing vs. shadow acne). This means any existing point lights which may have had a Bias set before that wasn't doing anything will now start having an effect, and this will change the shadow casting behaviour.

Spot lights that cast shadows now have a new slider which allows you to select the near clip distance. This is the distance to the light below which any objects won't cast shadows. Low values include close-by objects, at the cost of greatly reduced precision for the shadows. In previous Unity versions this was calculated at 4% of the total range of the light, which could be much too high for large lights. Now it defaults to 0.2, which should work for most cases.

Quaternion Mathematics
------------

The new support of importer Euler rotation curves, and the support of all the different Euler rotation orders necessitated a rewrite of the QuaternionToEuler and EulerToQuaternion mathematics functions, both in traditional and SIMD versions. Those new variations have not been made available in the API yet, and are only used internally for now.

This should have very little impact, but there are minute differences (<0.01 degrees) in the results between the previous version and the new one, and only when very close to gimbal lock conditions. Tests run have shown the new version to be more accurate most of the time, and the average error to be smaller by at least a factor of 10.

JointDriveMode flags
-------------
JointDriveMode flags are now obsolete, and thus have been removed. However, in earlier versions of Unity they were incorrectly being used to ignore the Configurable Joint's Joint Drive stiffness and damping settings. When upgrading a project to Unity 5.3 which uses Configurable Joints, users should be aware that these settings may now be having an effect when previously they did not - because they were wrongly being ignored based on the old JointDriveMode flags.


Legacy Light Animation
-------------
As of 5.3, Legacy Animations, both existing and new, will not animate Light properties. Changes to the underlying data structure of the Lights have made them incompatible with Legacy. To properly animate Lights, please use the Animator Component.=======

Editor Extensions
-------------
The scene's dirty flag is now respected when saving scenes. Editor extensions that do not correctly set the dirty flag may fail to save data correctly. Use Undo.RecordObject to record that an object is about to change and to update the scene’s dirty flag accordingly, or EditorSceneManager.MarkSceneDirty to forcibly mark the entire scene as dirty.

Camera Depth Texture shader variable
-------------
The `_CameraDepthTexture` shader variable has been fixed to consistently refer to the primary depth texture on the camera, and not as it did previously to the last depth texture rendered by any camera. If you are rendering a secondary camera in a script to e.g. obtain a half-resolution depth buffer and you need to bind its depth texture, you should now use the `_LastCameraDepthTexture` variable which has the semantics of referring to the depth texture of whichever camera rendered last.

##ComputeBuffers

The data layout of ComputeBuffers in automatically-converted OpenGL shaders has changed to match the layout of DirectX ComputeBuffers. If you use ComputeBuffers in OpenGL, remove any code that tweaks the data to match the previous OpenGL-specific layout rules. Please see [Compute Shaders](ComputeShaders) for more information.
