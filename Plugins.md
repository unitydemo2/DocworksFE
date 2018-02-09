#Plugins

In Unity, you normally use scripts to create functionality but you can also include code created outside Unity in the form of a __Plugin__. There are two kinds of plugins you can use in Unity: _Managed plugins_  and _Native plugins_.



_Managed plugins_ are managed .NET assemblies created with tools like Visual Studio or MonoDevelop. They contain only .NET code which means that they can't access any features that are not supported by the .NET libraries. However, managed code is accessible to the standard .NET tools that Unity uses to compile scripts. There is thus little difference in usage between managed plugin code and Unity script code, except for the fact that the plugins are compiled outside Unity and so the source may not be available.

_Native plugins_ are platform-specific native code libraries. They can access features like OS calls and third-party code libraries that would otherwise not be available to Unity. However, these libraries are not accessible to Unity's tools in the way that managed libraries are. For example, if you forget to add a managed plugin file to the project, you will get standard compiler error messages. If you do the same with a native plugin, you will only see an error report when you try to run the project.

This section explains how to create plugins and use them in your Unity projects.

