Building Plugins for Tizen
========================


This page describes [Native Code Plugins](Plugins) for the Tizen platform.


Building an Application with a Native Plugin for Tizen
----------------------------------------------------


1. Define your extern method in the C# file as follows:


````
[DllImport ("PluginName")]
private static extern float FooPluginFunction();
````

1. Set the editor to the Tizen build target
2. Create a Tizen Native Shared Library project from the Tizen IDE.
3. All native functions that you want to use from managed code need to have the EXPORT_API attribute added to their definitions. The header tizen.h also needs to be included for access to the EXPORT_API macro.

````
#include <tizen.h>

EXPORT_API float FooPluginFunction();
````

If you are using C++ (.cpp) to implement the plugin you must ensure the functions are declared with C linkage to avoid [name mangling issues](http://en.wikipedia.org/wiki/Name_mangling). 



````
extern "C" {
  EXPORT_API float FooPluginFunction();
}
````

Plugins written in C do not need this since these languages do not use name-mangling.

Using Your Plugin from C#
-------------------------


Once built, the shared library should be copied to the __Assets-&gt;Plugins-&gt;Tizen-&gt;libs__ folder. Unity will then find it by name when you define a function like the following in the C# script:



````
[DllImport ("PluginName")]
private static extern float FooPluginFunction ();

````

Please note that __PluginName__ should not include the prefix ('lib') nor the extension ('.so') of the filename.
You should wrap all native code methods with an additional C# code layer. This code should check [Application.platform](ScriptRef:Application-platform.html) and call native methods only when the app is running on the actual device; dummy values can be returned from the C# code when running in the Editor. You can also use [platform defines](PlatformDependentCompilation) to control platform dependent code compilation.

Calling C# / JavaScript back from native code
---------------------------------------------

Unity Tizen supports limited native-to-managed callback functionality via _UnitySendMessage_:

````
UnitySendMessage("GameObjectName1", "MethodName1", "Message to send");
````
This function has three parameters : the name of the target GameObject, the script method to call on that object and the message string to pass to the called method.

Known limitations:

1. Only script methods that correspond to the following signature can be called from native code: ` function MethodName(message:string)`
1. Calls to _UnitySendMessage_ are asynchronous and have a delay of one frame.


