#Upgrading to 64 bit iOS

iOS 64 bit support is implemented with the scripting backend called IL2CPP. It runs with your C#/UnityScript code.

The IL2CPP runtime combines an ahead of time compiler with a virtual machine to convert assemblies to C++ while leveraging standard platform C++ compilers to produce native binaries. The net result is significantly higher performance, platform compatibility and maintainability.

IL2CPP is the only scripting backend to support deploying to ARM 64-bit on iOS, and is thus mandatory to deploy to the Apple app-store for releasing new apps.

To read more about IL2CPP see the blogposts [The future of scripting in Unity](http://blogs.unity3d.com/2014/05/20/the-future-of-scripting-in-unity/), and [Apple iOS 64-bit support in Unity](http://blogs.unity3d.com/2014/11/20/apple-ios-64-bit-support-in-unity/).

##How to start using IL2CPP on iOS

Pick it in __Scripting Backend__ dropdown in [Player Settings](class-PlayerSettings).

![Scripting backend selection](../uploads/Main/ScriptingBackendSelection.png)

By default it will build for __Universal__ architecture (including both _ARM64_ and _ARMv7_), if needed you might switch to specific architecture in [Player Settings](class-PlayerSettings). There is number of things that should be done before your application is up and running in 64 bits:

* You need 64 bit capable device to test on. These are all iOS devices with A7 or later chip (currently these are: iPhone 5S, iPad Air, iPad Mini Retina, iPhone 6, iPhone 6 Plus, iPad Mini 3, iPad Air 2).
* You need all your native plugins to be compiled with 64 bit support (or be provided as source code). If you are using 3rd party plugin, you should contact your plugin vendor to obtain 64 bit capable and IL2CPP compatible version of that plugin. At the moment all latest Prime31 plugins are known to be good.
* If you are the plugin vendor or just have your own native plugins then you need keep couple of things in mind:
    * IL2CPP is not API-compatible (which is unexposed) with the Mono Runtime API, which means if plugin is using _mono\_\*_ functions won't link anymore. The best way to resolve this issue is to switch to managed delegate/callback approach and pass your managed callbacks to the native side of plugin and call them back from there when some native data or event arrives.
    * All plugins that come as precompiled static libraries (.a files) should now include _ARM64_ slice.
    * When doing native code/type conversion keep in mind that pointers and longs are now 64 bit wide and ints are still 32 wide.
* To minimise generated amount of C++ code IL2CPP is always (even when _Stripping level_ is set to __Disabled__) doing some sort of managed code stripping. Sometimes you will need to help it. Look for [link.xml](iphone-playerSizeOptimization) guide in iOS player size optimization manual.

##Troubleshooting
* Q: My code is running slower on IL2CPP than on Mono. Why?  
A: Make sure you are testing your code performance in Xcode _*Release*_ configuration. If issue still remains, please submit a bugreport! 
* Q: Unity generated Xcode project fails to compile with following or similar error: `Method not found: 'Default constructor not found...ctor() of System.ComponentModel.Int64Converter'`.   
A: Deserializers and serializers often reference some types only via .NET Reflection API and in such cases these methods or even classes might be stripped from project. You can hint managed code stripper that specific class / method is used either via [link.xml](iphone-playerSizeOptimization) or via introduction of dummy code that explicitly references it in one of your scripts.
* Q: Unity generated Xcode project fails to compile with some other error.  
A: Please verify if all your plugins support _ARM64_ and IL2CPP and if that’s the case please submit a bug report and attach your project (or just scripting part of it) to the bug report. Thanks!





