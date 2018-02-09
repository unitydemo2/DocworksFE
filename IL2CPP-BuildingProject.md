# Building a project using IL2CPP

To build your project using IL2CPP, open the [Build Settings](BuildSettings) window (__File __> __Build Settings__). Select the platform you are building for, then click __Player Settings...__ to open the [PlayerSettings](class-PlayerSettings) window in the [Inspector](UsingTheInspector).

![The Build Settings window](../uploads/Main/IL2CPP-1.png)

In the PlayerSettings window for your [target platform](PlatformSpecific), scroll down to the __Configuration__ section. For __Scripting Backend__, select  __IL2CPP__.

![The Configuration section of the PlayerSettings window](../uploads/Main/IL2CPP-2.png)

With IL2CPP selected as the Scripting back end, click __Build__ in the Build Settings window. Unity begins the process of converting your C# code and assemblies into C++ before producing a binary file for your target platform.