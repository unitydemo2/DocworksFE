#Upgrading to Unity 5.4

When upgrading projects from Unity 5.3 to Unity 5.4, there are some changes you should be aware of which may affect your existing project.


##Networking: Multiplayer Service API changes

[Numerous changes to the Networking API](UpgradeGuide54Networking).

##Networking: WebRequest no longer experimental

The `WebRequest` interface has been promoted from `UnityEngine.Experimental.Networking` to `UnityEngine.Networking`. Unity 5.2 and 5.3 projects that use `UnityWebRequest` will have to be updated.

##Scene View: Tone mapping not automatically applied

An image effect with the `ImageEffectTransformsToLDR` attribute will no longer be applied directly to the Scene view if found. A new attribute exists for applying effects to the Scene view: `ImageEffectAllowedInSceneView`. The 5.4 Standard Assets have been upgraded to reflect this change. 

##Shaders: Renamed variables

A number of built-in shader variables were renamed for consistency:

- **\_Object2World** and **\_World2Object** are now **unity_ObjectToWorld** and **unity_WorldToObject**
- **\_World2Shadow** is now **unity_WorldToShadow[0]**, **\_World2Shadow1** is **unity_WorldToShadow[1]** etc.
- **\_LightMatrix0** is now **unity_WorldToLight**
- **\_WorldToCamera**, **\_CameraToWorld**, **\_Projector**, **\_ProjectorDistance**, **\_ProjectorClip** and **\_GUIClipTextureMatrix** are now all prefixed with **unity**

The variable references will be automatically renamed in .shader and .cginc files when importing them. However, after the import the shaders will not be usable in Unity 5.3 or earlier, without manually renaming the variables.

##Shaders: Uniform arrays

In Unity 5.4, the way arrays of shader properties are handled has changed. Now there is "native" support for float/vector/matrix arrays in shaders (via `MaterialPropertyBlock.SetFloatArray`, `Shader.SetGlobalFloatArray` etc.). These new APIs allow arrays up to 1,023 elements.

The old way of using number-suffixed names for referring to individual array elements is deprecated (e.g. `_Colors0`, `_Colors1`) in both `Material` and `MaterialPropertyBlock`. Properties of this kind, serialized with the `Material` are no longer able to set array elements (but if any uniform array's name is suffixed by a number it still works).

## Shaders: Miscellaneous changes in 5.4

The default shader compilation target has changed to "#pragma target 2.5" (SM3.0 on DX9, DX11 9.3 feature level on WinPhone). You can still target DX9 SM2.0 and DX11 9.1 feature level with "#pragma target 2.0". 

The majority of built-in shaders target 2.5 now: Notable exceptions are Unlit, VertexLit and fixed function shaders. In practice, this means that most of built-in shaders and newly-created shaders, by default, will not work on PC GPUs that are made before 2004. See [this blog post](http://blogs.unity3d.com/2015/08/27/plans-for-graphics-features-deprecation/) for details.

The `Material` class constructor `Material(string)`, which was already deprecated, stops working in 5.4. Using it will print an error and result in the magenta error shader.

The internal shader used to compute screen-space directional light shadows has moved to Graphics Settings. If you were using a customized version of directional light shadows by having a copy of that shader in your project, it will no longer be used. Instead, select your custom shader under __Edit > Project Settings > Graphics__.

Reflection probes share a sampler between the two textures. If you are sampling them manually in your shader, and get an  "undeclared identifier samplerunity_SpecCube1" error, you’ll need to change code from `UNITY_PASS_TEXCUBE(unity_SpecCube1)` to `UNITY_PASS_TEXCUBE_SAMPLER(unity_SpecCube1,unity_SpecCube0)`.

`UnityEditor.ShaderUtil.ShaderPropertyTexDim` is deprecated; use `Texture.dimension`.

##ComputeBuffers

The data layout of ComputeBuffers in automatically-converted OpenGL shaders has changed to match the layout of DirectX ComputeBuffers. If you use ComputeBuffers in OpenGL, remove any code that tweaks the data to match the previous OpenGL-specific layout rules. Please see [Compute Shaders](ComputeShaders) for more information.

##Playables: Migrating to 5.4

* Playables are now structs instead of classes.

* The `Playable` structs are handles to native `Playable` classes, instead of pointers to native `Playable` classes.

* A non-null `Playable` struct doesn’t guarantee that the Playable is usable. Use the `.IsValid` method to verify that your Playable can be used.

* Any method that used to return null for empty inputs/outputs will now return `Playable.Null`.

* `Playable.Null` is an invalid Playable.

* `Playable.Null` can be passed to `AddInput`, `SetInput` and `SetInputs` to reserve empty inputs, or to implicitly disconnect connected inputs.

* Using `Playable.Null` or any invalid Playable as an input to any method, or calling a method on an invalid Playable will throw appropriate exceptions for the operation.

* Comparing Playables with `null` is now meaningless. Compare with `Playable.Null`.

* Playables must be allocated using the `Create` static method of the class you wish to use.

* Playables must be de-allocated using the `.Destroy` method on the Playable handle.

* Playables that are not de-allocated will leak.

* Playables were converted to structs to improve performance by avoiding boxing/unboxing ([more info on boxing](https://msdn.microsoft.com/en-us/library/yz2be5wk.aspx)). 

* Casting a `Playable` to an object, implicitly or explicitly, will cause boxing/unboxing, thus reducing performance.

* Inheriting from a Playable class will cause boxing/unboxing of instances of the child class.

* Since only animation is available for now, `ScriptPlayable`s have been replaced by `CustomAnimationPlayables`.

* It is no longer possible to derive from base Playables. Simply aggregate Playables in your custom Playables.


##Oculus Rift: Upgrading your project from Unity 5.3

Follow these instructions to upgrade your Oculus VR project from Unity 5.3:

Re-enable virtual reality support.

* Open the [Player Settings](class-PlayerSettings). (Menu: __Edit &gt; Project Settings &gt; Player__)
* Select __Other Settings__ and check the __Virtual Reality Supported__ checkbox. Use the Virtual Reality SDK list displayed below the checkbox to add and remove Virtual Reality Devices for each build target. 

Remove  __Oculus Spatializer__.

* Remove the __Oculus Spatializer__ Audio Plugin from your project through the Audio Settings Window (Menu: __Edit &gt; Project Settings &gt; Audio__), using the Spatializer Plugin dropdown. It may conflict with the native spatializer and prevent building.

##Reordering siblings

There has been a change to the events that are triggered when sibling GameObjects are re-ordered in Unity 5.4. Sibling GameObjects are GameObjects which all share the same parent in the Hierarchy window. In prior versions of Unity, changing the order of sibling GameObjects would cause every sibling to receive an `OnTransformParentChanged` call. In 5.4, the sibling GameObjects no longer get this call. Instead, the parent GameObject receives a single call to `OnTransformChildrenChanged`. 

This means that if you have code in your project that relies on __OnTransformParentChanged__ being called when siblings are re-ordered, these calls will no longer occur, and you need to update your code to take action when the parent object receives the __OnTransformChildrenChanged__ call instead.

This changed because the new behavior gives improved performance.

##Rearranging large GameObject hierarchies at runtime
Due to optimisations in the Transform component, using `Transform.SetParent` or `Destroy`ing parts of hierarchies involving 1000+ GameObjects may now take a long time. Calling `SetParent` on or otherwise rearranging such large hierarchies at runtime is not recommended.

##Windows Store

The generated Visual Studio project format was updated for all .NET scripting backend SDKs. This fixes excessive rebuilding when nothing has changed in the generated project. You might need to delete your existing generated *.csproj, especially if it was built with the “Generate C# projects” option checked, so Unity can regenerate it.

##Script serialization errors

There are two new script serialization errors to catch when the Unity API is being called from constructors and field initializers during deserialization (loading). Deserialization might happen on a different thread to the main thread and it is therefore not safe to call the Unity API during deserialization. There are more details at the bottom of the (Script Serialization)[script-Serialization] page in the Unity Manual.

##Supporting Retina screens

The editor now supports Retina resolutions on Mac OS X with high-resolution text, UI and 3D views.

The Editor GUI is now defined in point space rather than pixel space. On standard resolution displays, there is no change because each point is one pixel. On Retina displays, however, every point is two pixels. The current screen to UI scale is available as `EditorGUIUtility.pixelsPerPoint`. Since Unity can have multiple windows, each on monitors with different pixel densities, this value might change between views. 

If your editor code uses regular Editor/GUI/Layout methods, it is quite likely that you will not need to change anything.

If you are using `Screen.width/height`, switch to `EditorWindow.position.width/height` instead. This is because screen size is measured in pixels, but UI is defined in points. For custom Editors displaying in the Inspector, use `EditorGUIUtility.currentViewWidth`, which properly accounts for the presence of a scroll bar.

If you are displaying other content in your UI, such as a RenderTexture, you are probably calculating its size in points. To support Retina resolutions, you will need to convert your point sizes to pixel sizes. There are new methods in [EditorGUIUtility](ScriptRef:EditorGUIUtility.html) for this.

If you are using GUIStyles with custom backgrounds, you can add Retina versions of background textures by putting one texture with exactly doubled dimensions into a 'GUIStyleState.scaledBackgrounds' array.

Macs with underpowered graphics hardware may experience unacceptably slow editor frame rates in 3D views due to increased resolution. Retina support can be disabled by choosing "Get Info" on Unity.app in the Finder, and checking "Open in Low Resolution".


##Physics: Meshes and physics transform drift


There are:

* Changes to reject physics meshes if they contain invalid (non-finite) vertices.
* Changes to avoid physics transform drift by not sending redundant Transform updates.

The 5.3 behavior is that the animation system always sends Transform update messages for animation curves which are constant. These messages wake up the Rigidbodies and fixing this proved very risky in 5.3.

The 5.4 behavior is that if there are no position changes, the Rigidbody does not wake up (as most people would expect).

If your project relies on the 5.3 behavior of waking Rigidbody all the time, it might not work as expected in 5.4. 

##Web Player

The Unity Web Player target has been dropped from Unity 5.4. If you upgrade your project to 5.4, you will not be able to deploy it to the Web Player platform.

If you have legacy Web Player projects that you need to maintain, do not upgrade them to 5.4 or later.
 