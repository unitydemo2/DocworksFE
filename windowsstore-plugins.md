#Universal Windows Platform: Plugins on .NET Scripting Backend

## Universal Windows Platform plug-in settings

To view these settings, go to the Unity Editor's Project Window, select the plug-in file, then in the Inspector window navigate to __Platform settings__ &gt; __Universal Windows Platform__ (the Windows icon).

![Universal Windows Platform plug-in settings](../uploads/Main/PluginInspectorWSATab.png)

|**_Property:_** |**_Function:_** |
|:---|:---|
|__SDK__ |Use the drop-down to make the plug-in compatible with __Any SDK__ or specific SDKs. |
|__CPU__ |Use the drop-down to make the plug-in compatible with __Any CPU__, or limit the plug-in to __32-bit__, __64-bit__ or __ARM__ players. |
|__Don't process__ <br/>(Only applies for managed assemblies) |Tick this checkbox to disable patching for this assembly. Assemblies need patching when they contain classes serializable by Unity. In these cases, Unity injects additional IL code into the assemblies. If you know the assemblies doesn't have these classes, then it's safe to disable patching. <br/>**Note:**  Unity injects serialization code into your assemblies, so if you have a class derived from MonoBehaviour in your plug-in, and Unity doesn't patch it, you might get a serialization error during runtime. |
|__Placeholder__ <br/>(Only applies for managed assemblies) | With Universal Windows Platform you can have plug-ins compiled against .NET Core, but because the Unity Editor runs on Mono, it fails to recognize these assemblies. As a result, C# or JS files can't reference them. To work around this, you need to provide an assembly compiled against .NET 3.5 with identical API, which acts as a placeholder for the real plugin (see next section, _Placeholder plug-ins_). |

See documentation on the [Plugin Inspector](PluginInspector) for more information.

## Placeholder plug-ins

You cannot use Universal Windows Platform-specific plugins in the Unity Editor if you use [Windows Runtime APIs](http://msdn.microsoft.com/en-us/library/windows/apps/br211377.aspx). This section describes how the to handle this in the Unity Editor. 

If you only intend to use the plugin for Universal Windows Platform, and not in the Unity Editor, you don't need to make a placeholder, but you do need to wrap the code which uses the plugin API with the following:

```
#if !UNITY_EDITOR
// Plugin code
#endif
```

If you intend to use the plugin for both Universal Windows Platform and the Unity Editor, you need a placeholder. Make two plugins:

* For **Universal Windows Platform**, an assembly plug-in compiled against .NET Core with Windows Runtime API inside.
* For the **Unity Editor**, an assembly plug-in compiled against .NET 3.5, which has identical public API with dummy function implementations (this is the placeholder).

Both plug-ins must share the same name and have the same assembly version. Note that the placeholder plugin for the Unity Editor cannot reference _UnityEditor.dll_. if it does, Unity generates an error.

The steps below describe how to assign a platform to each in the Editor.

1. In the Unity Editor's Project window, select your Editor-compatible placeholder plug-in. In the Inspector window, go to __Select platforms for plugin__ and select __Editor__ as the only compatible platform.

1. In the Unity Editor's Project window, select your Universal Windows Platform-compatible placeholder plug-in. In the Inspector window, go to __Select platforms for plugin__ and select __Universal Windows Platform__ as the only compatible platform.

1. In the Inspector window for the Universal Windows Platform-compatible plug-in, set the __Placeholder__ field to your Editor-compatible placeholder plug-in.

This means that when building to Universal Windows Platform, Unity uses Editor-compatible placeholder plug-in when compiling your scripts, but copies the Universal Windows Platform-compatible plug-in to the final folder. This achieves two things: The Unity Editor successfully compiles your scripts, but the built game itself still uses the API from the Universal Windows Platform-specific plug-in.

---
<span class="page-edit">• 2017-05-16  <!-- include IncludeTextAmendPageSomeEdit --></span><br/>
