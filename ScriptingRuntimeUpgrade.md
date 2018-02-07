#Scripting Runtime Upgrade
For 2017.1 the option to use .NET 4.6 will be an experimental, per project option. This option is in the GUI as a Player Setting above __Scripting Backend__ and __Api Compatibility Level__:

![](../uploads/Main/ScriptingRunetimePreview.png)

The equivalent scripting API is the __PlayerSettings.scriptingRuntimeVersion__ property. __Note that changing this setting requires an Editor restart since it affects the Editor as well as players.__

By default nothing should change about how Unity behaves or what .NET functionality is available. Once you opt-in to the new .NET 4.6 for a project, you will be able to use C# 6, .NET 4.6 class libraries, and new runtime features in user scripts and precompiled assemblies.

## FAQ

### What platforms does this affect?

All of them, but in different ways:

- Editor and Standalone use the new version of Mono when this option is enabled.

- All console platforms will only be able to use IL2CPP when targeting the new .NET version.

- iOS and WebGL will continue to be IL2CPP only.

- Android will continue to support both Mono and IL2CPP.

- Other platforms are still undergoing work to support either new Mono or IL2CPP

*At the current time (2017.1b4) please focus on using this option on desktop, iOS, and Android. Support for other platforms is still under development.*

### What about IL2CPP?

IL2CPP fully supports the new .NET 4.6 APIs and features.

### How stable is the updated Mono/IL2CPP?

The internal, automated tests for Unity pass with the new Mono/IL2CPP. Of course, we still expect you may encounter issues. Please file bugs for any issues you encounter.

### Does this preview include a new GC?

No. This is an upgrade of the class libraries and runtime, but we are still using the Boehm GC. We are targeting a new version of Boehm that we use with IL2CPP (so IL2CPP and Mono will have exact same GC).

### Wait, why don't we have a new GC?

The newer Mono garbage collector (SGen) requires additional work in Unity and will follow once we have stabilized the new runtime and class libraries.

### Can I debug managed code with this new Mono?

VSTU 3.1 is required for our new Mono. Please install it to use the new Mono runtime on Windows.

MonoDevelop currently cannot debug the new Mono runtime, but we are working to fix this.

### Why are my builds larger with the new .NET version?

The .NET 4.6 class libraries are quite larger than our current .NET 3.5 class libraries. We are actively working on improving the managed linker to reduce size further.

Additionally, we are working on a new Unity specific class library API profile (like our current __unity__ profile) that will

a) be specifically implemented to work on AOT platforms

b) smaller in surface area and internally designed to be strippable/linkable

c) support [netstandard 2.0](https://github.com/dotnet/standard/blob/master/docs/netstandard-20/README.md) (yet to be officially released)

### When I try this new option, something doesn't work. What should I do?

Please file a bug. We will be rapidly fixing them!

----

*  <span class="page-edit">2017-05-24  <!-- include IncludeTextNewPageNoEdit --></span>
  
* <span class="page-history">New feature in Unity [2017.1](../Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>
