# Windows Store: Generated project with IL2CPP scripting backend

Building a project from Unity to Windows Store platform with IL2CPP scripting backend will create a Visual Studio C++ solution containing three projects:

![Figure 1. Generated Visual Studio solution](../uploads/Main/windowsstore-generatedsolution-il2cpp.png)

These projects serve their own purposes:

1. **Il2CppOutputProject** contains generated C++ code that was converted from managed assemblies. This project gets overwritten every time when built over it. See figure 2.
2. **Unity Data** project contains all Unity data files: levels, assets, etc. This project gets overwrriten every time as well.
3. The main project (it name matches your Unity project name). This is the project that will be built into an application package, which may be deployed to a device or uploaded to the Windows Store. Unity will not overwrite this project when built on top of it, so it can be modified freely without the fear of changes becoming lost.

![Figure 2. Il2CppOutputProject](../uploads/Main/windowsstore-il2cppoutputproject.png)

When using .NET scripting backend, the generated project is using C#, however, this scenario is unsupported when using IL2CPP scripting backend. 

###Configurations

Generated Visual Studio projects have three configurations: **Debug**, **Release** and **Master**:

* **Debug** configuration has all optimizations disabled, all debugging info preserved and runs much slower. It is used for debugging your game.
* **Release** configuration enables most code optimizations, but leaves profiler enabled. This configuration is used for profiling your game.
* **Master** configuration disables the profiler, and is used for game submission/final testing. The build time of **Master** configuration is much longer, however, it is a little bit faster than Release configuration.