Building Plugins for Desktop Platforms
======================================


This page describes [Native Code Plugins](Plugins) for desktop platforms (Windows/Mac OS X/Linux).


Building a Plugin for Mac OS X
------------------------------


On Mac OSX, [plugins](Plugins) are deployed as bundles. You can create the bundle project with XCode by selecting __File-&gt;NewProject...__ and then selecting __Bundle__ -&gt; __Carbon/Cocoa Loadable Bundle__ (in XCode 3) or __OS X__ -&gt; __Framework & Library__ -&gt; __Bundle__ (in XCode 4)

If you are using C++ (.cpp) or Objective-C (.mm) to implement the plugin then you must ensure the functions are declared with C linkage to avoid [name mangling issues](http://en.wikipedia.org/wiki/Name_mangling).



````
extern "C" {
  float FooPluginFunction ();
}

````

Building a Plugin for Windows
-----------------------------


Plugins on Windows are DLL files with exported functions. Practically any language or development environment that can create DLL files can be used to create plugins. 
As with Mac OSX, you should declare any C++ functions with C linkage to avoid name mangling issues.

Building a Plugin for Linux
---------------------------


Plugins on Linux are `.so` files with exported functions. These libraries are typically written in C or C++, but any language can be used. 
As with the other platforms, you should declare any C++ functions with C linkage in order to avoid name mangling issues.

32-bit and 64-bit libraries
---------------------------

The issue of needing 32-bit and/or 64-bit plugins is handled differently depending on the platform.

###Windows and Linux
On Windows and Linux, plugins can be managed manually (e.g, before building a 64-bit player, you copy the 64-bit library into the `Assets/Plugins` folder, and before building a 32-bit player, you copy the 32-bit library into the `Assets/Plugins` folder) OR you can place the 32-bit version of the plugin in `Assets/Plugins/x86` and the 64-bit version of the plugin in `Assets/Plugins/x86_64`. By default the editor will look in the architecture-specific sub-directory first, and if that directory does not exist, it will copy plugins from the root `Assets/Plugins` folder instead.

Note that for the Universal Linux build, you are required to use the architecture-specific sub-directories (when building a Universal Linux build, the Editor will not copy any plugins from the root `Assets/Plugins` folder).

###Mac OS X
For Mac OS X, you should build your plugin as a universal binary that contains both 32-bit and 64-bit architectures.

Using your plugin from C#
-------------------------


Once built, the bundle should be placed in the __Assets-&gt;Plugins__ folder (or the appropriate architecture-specific sub-directory) in the Unity project. Unity will then find it by name when you define a function like this in the C# script:-



````
[DllImport ("PluginName")]
private static extern float FooPluginFunction ();

````

Please note that __PluginName__ should not include the library prefix nor file extension. For example, the actual name of the plugin file would be PluginName.dll on Windows and libPluginName.so on Linux. 
Be aware that whenever you change code in the Plugin you will need to recompile scripts in your project or else the plugin will not have the latest compiled code.

Deployment
----------


For cross platform plugins you must include the .bundle (for Mac), .dll (for Windows), and .so (for Linux) files in the Plugins folder. 
No further work is then required on your side - Unity automatically picks the right plugin for the target platform and includes it with the player.


Examples
--------


###Simplest Plugin
This plugin project implements only some very basic operations (print a number, print a string, add two floats, add two integers). This example may be helpful if this is your first Unity plugin. 
The project can be found [here](../uploads/Examples/SimplestPluginExample-4.0.zip) and includes Windows, Mac, and Linux project files.

###Rendering from C++ code
An example multiplatform plugin that works with multithreaded rendering in Unity can be found on the [Native Plugin Interface](NativePluginInterface) page.

