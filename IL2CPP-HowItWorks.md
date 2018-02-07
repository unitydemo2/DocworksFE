# How IL2CPP works

Upon starting a build using [IL2CPP](IL2CPP), Unity automatically performs the following steps: 

1. Unity Scripting API code is compiled to regular .NET DLLs (managed assemblies).

2. All managed assemblies that aren’t part of scripts (such as plugins and base class libraries) are processed by a Unity tool called Unused Bytecode Stripper, which finds all unused classes and methods and removes them from these DLLs (Dynamic Link Library). This step significantly reduces the size of a built game.

3. All managed assemblies are then converted to standard C++ code.

4. The generated C++ code and the runtime part of IL2CPP is compiled using a native platform compiler.

5. Finally, the code is linked into either an executable file or a DLL, depending on the platform you are targeting.

![A diagram of the automatic steps taken when building a project using IL2CPP](../uploads/Main/IL2CPP-3.png)

IL2CPP provides a few useful options which you can control by attributes in your scripts. See documentation on [Platform-dependent compilation](PlatformDependentCompilation) for further information.