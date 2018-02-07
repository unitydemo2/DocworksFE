#Upgrading to Unity 2017.2

<!-- Change submissions: https://docs.google.com/document/d/19UVEduEfbR6gjxQrl3Ob-0Wo4gGTilKUBU10lLpMNzM/edit -->

This page lists any changes in 2017.2 which might affect existing projects when you upgrade from earlier versions of Unity.

For example:

* Changes in data format which may require re-baking.

* Changes to the meaning or behavior of any existing functions, parameters or component values.

* Deprecation of any function or feature. (Alternatives are suggested.)

***

**MonoBehaviour.OnValidate is now called when MonoBehaviour is added to a GameObject in the Editor**

MonoBehaviour.OnValidate is called when a Scene loads, when GameObjects are duplicated or when a value changes in the Inspector. It is now also called when adding a MonoBehaviour to a GameObject in the Editor.


***

**Scripting: InitializeOnLoad callback now invoked after deserialization**

The callback timing for InitializeOnLoad has changed. It was previously invoked at a point that could lead to invalid object states for existing serialized objects when calling Unity API. It is now invoked after deserialization and after all objects have been created. As part of the creation of objects, the default constructor must be invoked. This change means that objects constructors are now invoked before InitializeOnLoad static constructors, whereas InitializeOnLoad was previously called before some object constructors.

Example:

```
[System.Serializable]
public class SomeClass
{
    public SomeClass()
    {
        Debug.Log("SomeClass constructor");
    }
}

public class SomeMonoBehaviour : MonoBehaviour
{
    public SomeClass SomeClass;
}

[InitializeOnLoad]
public class SomeStaticClass
{
    static SomeStaticClass()
    {
        Debug.Log("SomeStaticClass static constructor");
    }
}
```

This would previously result in:<br/>
`SomeStaticClass static constructor` (InitializeOnLoad)<br/>
`SomeClass constructor` (object constructor)

After this change it will now be:<br/>
`SomeClass constructor` (object constructor)<br/>
`SomeStaticClass static constructor` (InitializeOnLoad)


***


**New normal map type that support BC5 format.**

Up to now Unity was supporting either RGB normal map or swizzled AG normal map (with x in alpha channel and y in green channel) with different compression format. There is now support for RG normal map (with x in red channel and y in green channel).
UnpackNormal shader function have been upgraded to allow to use RGB, AG and RG normal map without adding shader variants. To be able to do this, the UnpackNormal function rely on having unused channel of the normal map set to 1. I.e a swizzled AG normal map must be encoded as (1, y, 1, x) and a RG (x, y, 0, 1). Unity normal map encoder enforce it.

There is no upgrade to do if users were using unmodified Unity. However in case users have done their own normal map shaders or their own encoding, they may need to take into account the need for swizzled AG normal map to be encoded as (1, y, 1, x). In case users were mixing normal map in swizzled AG before unpacking normal map, they may require to use UnpackNormalDXT5nm instead of UnpackNormal.



***




**Always precompiled managed assemblies (.dlls) and assembly definition file assemblies on startup in the Editor.**

Load precompiled managed assemblies (.dlls) and assembly definition file assemblies on Editor startup even if there are compile errors in other scripts. This is useful for Editor extension assemblies that should always be loaded on startup, regardless of other script compile errors in the project.

***


**HDR emission.**

If you are using precomputed realtime GI or baked GI, intense emissive materials set up in earlier versions of Unity could look more intense now, because their range is not capped any more. The RGBM encoding used previously gave an effective range of 97 for gamma space and 8 for linear color space. The HDR color picker had a maximum range of 99 so some materials could be set to be more intense than they seemed.
After the upgrade, emission color is passed to the GI systems as true HDR 16 bit floating point values (range is now 64K). Internally, the realtime GI system is using the rgb9e5 shared exponent format that can represent these intense values but the baked lightmaps are limited by their RGBM encoding. HDR for baked lightmaps will be added in a later release.

***


**VR to XR rename.**

The UnityEngine.VR.* namespaces have been renamed to UnityEngine.XR.*.  All types with VR in their name have also been renamed to their XR versions.  For example: UnityEngine.VR.VRSettings is now UnityEngine.XR.XRSettings, etc.

The API updater has been configured to automatically update existing scripts and assemblies to the new type names and namespaces.  If don’t want to use the API updater, you can also manually update namespaces and types.

Namespace changes:

* UnityEngine.VR -> UnityEngine.XR
* UnityEngine.VR.WSA -> UnityEngine.XR.WSA
* UnityEngine.VR.WSA.Input -> UnityEngine.XR.WSA.Input
* UnityEngine.VR.WSA.Persistence -> UnityEngine.XR.WSA.Persistence
* UnityEngine.VR.WSA.Sharing -> UnityEngine.XR.WSA.Sharing
* UnityEngine.VR.WSA.WebCam -> UnityEngine.XR.WSA.WebCam

UnityEngine.VR type changes:

* VRDevice -> XRDevice
* VRNodeState -> XRNodeState
* VRSettings -> XRSettings
* VRStats -> XRStats
* VRNode -> XRNode

All `VR.*` profiler entries have also been changed to `XR.*`.

***

**UnityEngine.dll is now split into separate dlls for each UnityEngine module.**

The UnityEngine.dll (which contains all public scripting API) has been separated into modules of code covering different subsystems of the engine. This makes the Unity code base better organized with cleaner internal dependencies, better for internal tooling and makes the code base more strippable. The separated modules include UnityEngine.Collider which is now in UnityEngine.PhysicsModule.dll and UnityEngine.Font which is now in UnityEngine.TextRendering.dll.

This change should typically not affect any of your existing projects and your scripts now automatically compiles against the correct assemblies. Unity now includes a UnityEngine.dll assembly file containing [type forwarders](https://docs.microsoft.com/en-us/dotnet/framework/app-domains/type-forwarding-in-the-common-language-runtime) of all UnityEngine types for all pre-compiled assemblies referencing the DLL which ensures backwards compatibility by forwarding the files to their new locations.

However, there is one case where existing code might break from this change. That is if your code uses reflection to get UnityEngine types, and assumes that all types live in the same assembly. This means such code would fail, because Collider and Font are now in different assemblies:

```
System.Type colliderType = typeof(Collider);
System.Type fontType = colliderType.Assembly.GetType("Font");
```

Getting either Collider or Font types from the "UnityEngine" assembly still works due to the use of type forwarders, like this: 

```
System.Type.GetType("UnityEngine.Collider, UnityEngine")
```

Unity does still bundle a fully monolithic UnityEngine.dll which contains all UnityEngine APIs in the Unity Editor's Managed/UnityEngine.dll folder. This makes sure that any existing Visual Studio/MonoDevelop solutions referencing UnityEngine.dll continues to build without needing to be updated to reference the new modular assemblies. You should continue to use this assembly to reference UnityEngine API in your custom solutions, as the internal split of modules is subject to change.

***

**Material smoothness in Standard shader.**

Purely smooth materials that use the GGX version of the standard shader now receive specular highlights which increases the realism of such materials. 



----

* <span class="page-edit">2017-10-06  <!-- include IncludeTextNewPageNoEdit --></span>