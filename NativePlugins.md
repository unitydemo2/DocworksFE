#Native Plugins

Unity has extensive support for native __Plugins__, which are libraries of native code written in C, C++, Objective-C, etc. Plugins allow your game code (written in Javascript or C#) to call functions from these libraries. This feature allows Unity to integrate with middleware libraries or existing C/C++ game code.

In order to use a native plugin you firstly need to write functions in a C-based language to access whatever features you need and compile them into a library. In Unity, you will also need to create a C# script which calls functions in the native library.

The native plugin should provide a simple C interface which the C# script then exposes to other user scripts. It is also possible for Unity to call functions exported by the native plugin when certain low-level rendering events happen (for example, when a graphics device is created), see the [Native Plugin Interface](NativePluginInterface) page for details.


##Example

A very simple native library with a single function might have source code that looks like this:

````
	float FooPluginFunction () { return 5.0F; } 
````

To access this code from within Unity, you could use code like the following:

````
	using UnityEngine;
	using System.Runtime.InteropServices;

	class SomeScript : MonoBehaviour {

	   #if UNITY_IPHONE
   
	   // On iOS plugins are statically linked into
	   // the executable, so we have to use __Internal as the
	   // library name.
	   [DllImport ("__Internal")]

	   #else

	   // Other platforms load plugins dynamically, so pass the name
	   // of the plugin's dynamic library.
	   [DllImport ("PluginName")]
	
	   #endif

	   private static extern float FooPluginFunction ();

	   void Awake () {
		  // Calls the FooPluginFunction inside the plugin
		  // And prints 5 to the console
		  print (FooPluginFunction ());
	   }
	}
````

Note that when using Javascript you will need to use the following syntax, where DLLName is the name of the plugin you have written, or "__Internal" if you are writing statically linked native code:


````
	@DllImport (DLLName)
	static private function FooPluginFunction () : float {};
````

##Creating a Native Plugin

In general, plugins are built with native code compilers on the target platform. Since plugin functions use a C-based call interface, you must avoid name mangling issues when using C++ or Objective-C.


##Further Information

* [Native Plugin Interface](NativePluginInterface) (this is needed if you want to do rendering in your plugin)
* [Mono Interop with native libraries](http://www.mono-project.com/Interop_with_Native_Libraries)
* [P-invoke documentation on MSDN](http://msdn2.microsoft.com/en-us/library/fzhhdwae.aspx)
