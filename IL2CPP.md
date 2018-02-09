#IL2CPP

IL2CPP is a Unity-developed scripting back-end which you can use as an alternative to Mono when building projects for some platforms. When you choose to build a project using IL2CPP, Unity converts IL code (sometimes called CIL  - Intermediate Language or [Common Intermediate Language](https://en.wikipedia.org/wiki/Common_Intermediate_Language)) from scripts and assemblies into C++ code, before creating a native binary file (.exe, apk, .xap, for example) for your chosen platform. Some of the uses for IL2CPP include increasing the performance, security, and platform compatibility of your Unity projects. 

For more information about using IL2CPP, refer to the [The Unity IL2CPP blog series](https://blogs.unity3d.com/2015/05/06/an-introduction-to-ilcpp-internals/) and the following Unity Manual pages. 

* [Building a project using IL2CPP](IL2CPP-BuildingProject)
* [How IL2CPP works](IL2CPP-HowItWorks)
* [Optimising IL2CPP build times](IL2CPP-OptimizingBuildTimes)

Note - IL2CPP is only available when building for the following platforms:

* Android
* AppleTV
* iOS*
* Nintendo 3DS
* Nintendo Switch
* Playstation 4
* Playstation Vita
* WebGL*
* Windows Store
* Xbox One

*IL2CPP is the only scripting back end available when building for iOS and WebGL.