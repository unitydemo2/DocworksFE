# Windows Runtime support

Unity includes Windows Runtime support for [IL2CPP](IL2CPP) on Universal Windows Platform and Xbox One platforms. Use Windows Runtime support to call into both native system Windows Runtime APIs as well as custom .winmd files directly from managed code (scripts and DLLs).

To automatically enable Windows Runtime support in IL2CPP, go to PlayerSettings (__Edit__ > __Project Settings__ > __Player__), navigate to the __Configuration__ section, and set the __Api Compatibility Level__ to __.NET 4.6__.

![The __Configuration__ section of the PlayerSettings window.  The options shown above change depending on your chosen build platform.](../uploads/Main/IL2CPP-4.png)

Unity automatically references Windows Runtime APIs (such as _Windows.winmd_ on Universal Windows Platform) when it has Windows Runtime support enabled. To use custom .winmd files, import them (together with any accompanying DLLs) into your Unity project folder. Then use the [Plugin Inspector](PluginInspector) to configure the files for your target platform.

![Use the Plugin Inspector to configure custom .winmd files for specific platforms
](../uploads/Main/IL2CPP-5.png)

In your Unity project's [scripts](ScriptingSection) you can use the `ENABLE_WINMD_SUPPORT` #define directive to check that your project has Windows Runtime support enabled. Use this before a call to .winmd Windows APIs or custom .winmd scripts to ensure they can run and to ensure any scripts not relevant to Windows ignore them. Note, this is only supported in C# scripts. See the examples below. 

**Examples**

**`C#`**

````
void Start() {
  #if ENABLE_WINMD_SUPPORT
    Debug.Log("Windows Runtime Support enabled");
    // Put calls to your custom .winmd API here
  #endif
}
````

In addition to being defined when Windows Runtime support is enabled in IL2CPP, it is also defined in .NET when you set __Compilation Overrides__ to  __Use Net Core__.

![The Publishing Settings section of the PlayerSettings Inspector window, with __Compilation Overrides__ highlighted in red](../uploads/Main/IL2CPP-6.png)

---

<span class="page-edit">• 2017-05-16  <!-- include IncludeTextAmendPageNoEdit --></span><br/>