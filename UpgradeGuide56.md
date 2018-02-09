#Upgrading to Unity 5.6

This page lists any changes in 5.6 which might affect existing projects when you upgrade from earlier versions of Unity.

For example:

* Changes in data format which may require re-baking.

* Changes to the meaning or behavior of any existing functions, parameters or component values.

* Deprecation of any function or feature. (Alternatives are suggested.)

* * *

**Script serialization errors no longer work**

The script serialization errors introduced in Unity 5.4 and described in detail in this [blog post](https://blogs.unity3d.com/2016/06/06/serialization-monobehaviour-constructors-and-unity-5-4/), will always throw a managed exception from 5.6 onwards. 

Behaviour in Unity 5.5 is the same as in Unity 5.4.

* * *

**PlayerSettings.apiCompatibilityLevel deprecated**

This is now a per-platform setting. 
Use [PlayerSettings.SetApiCompatibilityLevel](ScriptRef:PlayerSettings.SetApiCompatibilityLevel) and [PlayerSettings.GetApiCompatibilityLevel](ScriptRef:PlayerSettings.SetApiCompatibilityLevel) instead. [PlayerSettings.apiCompatibilityLevel](PlayerSettings.apiCompatibilityLevel) will continue to function, but it will only affect the current active platform.

* * *

**Lighting changes**

Directional specular lightmap has been removed.

As a consequence, [LightmapsMode.SeparateDirectional](ScriptRef:LightmapsMode.SeparateDirectional) has been removed. Use  [LightmapsMode.CombinedDirectional](LightmapsMode.CombinedDirectional) instead. 

Here are the prefered ways to get specular highlights in Unity 5.6:

* For direct specular, stationary lights with real-time direct lighting provide high quality specular highlights in all modes but the subtractive one. Please see the *Mixed Lighting* documentation in the online [lighting](https://docs.unity3d.com/560/Documentation/Manual/LightingOverview.html) section of the 5.6 User Manual.

* For indirect specular, use [Reflection Probes](class-ReflectionProbe), [Screen Space Reflection ](https://github.com/Unity-Technologies/PostProcessing)[(SSR)](https://github.com/Unity-Technologies/PostProcessing), or both.

**Mixed mode lighting has evolved**

Mixed  mode lighting in Unity 5.5 has been replaced with stationary lighting modes in Unity 5.6. This implies a lot of changes, and we advise you to carefully read the *Lighting Modes*  documentation, and in particular the *Stationary Modes* draft documentation in the online [lighting](https://docs.unity3d.com/560/Documentation/Manual/LightingOverview.html) section of the 5.6 User Manual which details the newly available options.

Projects from pre-Unity 5.6 will be upgraded to **Subtractive** mode (see the *Subtractive Light Mode* in the online [lighting](https://docs.unity3d.com/560/Documentation/Manual/LightingOverview.html) section of the 5.6 User Manual. This is the closest match to the **Mixed** lighting from Unity 5.5. 

However this mode is the lowest quality mode for Unity 5.6, so try other modes to see if they are a better fit for your projects. We highly recommend the **Shadowmask** (see the *Shadowmask* page and the *Distance Shadowmask* page in the online [lighting](https://docs.unity3d.com/560/Documentation/Manual/LightingOverview.html) section of the 5.6 User Manual, especially if you were using the now-defunct Directional Specular lightmaps before).

The default for new Unity 5.6 projects is **Distance shadowmask** mode. (See the *Distance shadowmask* page in the online [lighting](https://docs.unity3d.com/560/Documentation/Manual/LightingOverview.html) section of the 5.6 User Manual).

**Light probes**

In Unity 5.6 you can no longer choose whether direct lighting is added to Light Probes from the lighting window. This now happens automatically based on the lights types and the stationary modes. This ensures that direct lighting is not missing and that there is no double lighting on dynamic objects using Light Probes, greatly simplifying the process.


* * *


**New GPU instancing workflow**

You must now check the new __Enable Instancing__ checkbox for all Materials used for GPU instancing. This is required for GPU instancing to work correctly.

Note that the checkbox is not  checked automatically as it's impossible for Unity to determine if a Material uses a pre-5.6 Shader.

![](../uploads/Main/upgradeguide56_1.png)


An upgrade error is also imposed on SpeedTree Assets to help you regenerate the SpeedTree Materials, so that you can have __Enable Instancing__ checked.

**Note:** The newly introduced procedural instancing Shaders (those with `#pragma instancing_options procedural:func`) don't require this change because Shaders with the `PROCEDURAL_INSTANCING_ON` keyword are not affected.


* * *

**Particle system changes**

`Custom Vertex Streams` in the Renderer Module may now require you to manually upgrade your Particle Systems, if you use the `Particles/Alpha Anim Blend` Shader. In this situation, it is sufficient to simply remove the duplicated UV2 stream.

This is required because, in some cases, the duplicated stream is needed to maintain backwards compatibility, so there is no fully reliable auto-upgrade solution. The Normal and AnimFrame streams are also not required, but causes no problems if they exist. The fixed Particle System setup should look like this:

![](../uploads/Main/upgradeguide56_2.png)

Secondly, the upgraded Emission Module will cause Animation Bindings attached the Burst Emission to be lost. It will be necessary to rebind those properties.


* * *

**Animator change**

__Animate Physics__: Rigidbodies attached to objects where the Animator has _Animate Physics_ selected  now have velocities applied to them when animated. This will give correct physical interactions with other physics objects, and bring the Animator in line with the behaviour of objects animated by the Animation Component.

This will affect how your animated Rigidbodies interact with other Rigidbodies (the Rigidbodies are moved instead of teleported every frame), so make sure to verify that your Animators with __Animate Physics __are behaving as you expect.

* * *

**Dynamic batching 2D sprites**

You should use dynamic batching in upgraded projects that contain 2D sprites. This avoids significant sprite rendering performance issues on devices with Adreno and Mali chipsets.

To use Dynamic Batching, open the PlayerSettings (menu: __Edit__ > __Project Settings__ > __Player__). Open the __Other Settings__ section and, under __Rendering__, tick the __Dynamic Batching__ checkbox and untick the __Graphics Jobs (Experimental)__ checkbox. Note that these are the default settings for projects created in 5.6.

Graphics Jobs should not affect dynamic batching, but can sometimes cause unexpected behaviors on platforms that use Vulkan and DirectX12.

***

**NUnit library updated**

The [Unity Test Runner](testing-editortestsrunner) uses a Unity integration of the NUnit library, which is an open-source unit testing library for .NET languages. In Unity 5.6, this integrated library is updated from version 2.6 to version 3.5. This update has introduced some breaking changes that might affect your existing tests. See the [NUnit update guide](https://github.com/nunit/docs/wiki/Upgrading) for more information.

***

<br/>
* <span class="page-edit"> 2017-05-19 <!-- include IncludeTextAmendPageYesEdit --></span>


