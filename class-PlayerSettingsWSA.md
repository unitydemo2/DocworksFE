#Universal Windows Platform Player Settings

This page details the __Player Settings__ specific to Universal Windows Platform. For a description of the general Player Settings, see documentation on [Player Settings](class-PlayerSettings).

![](../uploads/Main/WSA-PlayerSettings.png)


Most of these settings are transferred to the _Package.appxmanifest_ file when creating Visual Studio solution for the first time.

Note: If you build your project on top of the existing one, Unity won’t overwrite the _Package.appxmanifest_ file if it’s already present. That means if you change something in Player Settings, you should be sure to check _Package.appxmanifest_. If you want to regenerate _Package.appxmanifest_, delete it and rebuild your project from Unity.

To learn more, see Microsoft's documentation on [App package manifest](http://msdn.microsoft.com/en-us/library/windows/apps/br211474.aspx).

Settings from Packaging, Application UI, Tile, Splash screen, and Capabilities directly transfer to settings in the _Package.appxmanifest_ file.

**Supported orientations** from Player Settings are also populated to the manifest (Package.appxmanifest file in Visual Studio solution). On Universal Windows Apps Unity will reset orientation to the one you used in Player Settings, regardless what you specify in the manifest. This is because Windows itself ignores those settings on desktop and tablet computers. Note, that you can always change supported orientations using Unity scripting API.

##Certificate

Every Universal Windows App needs a certificate which identifies a developer, Unity will create a default certificate, if you won’t provide your own.

##Compilation

As you know, Unity uses Mono when compiling script files, and you can use the API located in .NET 3.5. Compilation Overrides allows you to use .NET for Universal Windows Platform (also known as .NET Core) in your C# files, the API is available here.

##When Compilation Overrides is set to:

* None - C# files are compiled using Mono compiler.
* Use .Net Core - C# files are compiled using Microsoft compiler and .NET Core, you can use Windows Runtime API, but classes implemented in C# files aren’t accessible from the JS language. Note: when using API from Windows Runtime, it’s advisable to wrap the code with ENABLE_WINMD_SUPPORT define, because the API is only avaible when building to Universal Windows Platform, and it’s not available in Unity Editor.
* Use .Net Core Partially - C# files not located in Plugins, Standard Assets, Pro Standard Assets folders are compiled using Microsoft compiler and .NET Core, all other C# files are compiled using Mono compiler. The advantage is that classes implemented in C# are accessible from the JS language.
Note: You won’t be able to test .NET Core API in Unity Editor, because it doesn’t have access to .NET Core, so you’ll be able to test the API only when running Universal Windows App.

**Note:** You cannot use .NET Core API in JS scripts.

Here’s a simple example of how to use .NET Core API in scripts.

````
string GetTemporaryFolder()
{
#if ENABLE_WINMD_SUPPORT
    return Windows.Storage.ApplicationData.Current.TemporaryFolder.Path;
#else
    return "LocalFolder";
#endif
}
````

##Misc

Unprocessed Plugins contains a list of plugins which are ignored by Unity’s preprocessing tools (like SerializationWeaver, AssemblyPreprocessor, rrw). Usually you don’t need to modify this list, unless you’re getting an error that Unity’s failed to preprocess your plugin.

If you add a plugin to this list, Unity won’t inject additional IL code into your assembly used for serialization purposes, but if your plugin isn’t referencing UnityEngine.dll, that’s fine, because Unity won’t serialize any data from your plugin.

##Independent Input Source
This allows you to enable an option for independent input source. Basically this makes your input more responsive, and usually you want this option to be enabled.

Low Latency Presentation API
Lets you enable Low Latency Presentation API, basically this create D3D11 swapchain with DXGI\_SWAP\_CHAIN\_FLAG\_FRAME\_LATENCY\_WAITABLE\_OBJECT flag, read more here and should increase input responsiveness. This option is disabled by default because on hardware with older GPU drivers, this option makes game laggy, if you enable this option - be sure to profile your game if the performance is still acceptable.

##Capabilities
These options are directly copied to Package.appxmanifest.

**Note:** If you build your game on top of previous package, Package.appxmanifest won’t be overwritten.

---
<span class="page-edit">• 2017-05-16  <!-- include IncludeTextAmendPageNoEdit --></span><br/>
