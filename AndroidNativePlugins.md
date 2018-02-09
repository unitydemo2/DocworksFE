#Native (C++) plug-ins for Android

Unity supports native plug-ins for Android written in C/C++ and packaged in a shared library (.so).

To build a C++ plug-in for Android, use the [Android NDK](https://developer.android.com/ndk/index.html) and get yourself familiar with the steps required to build a shared library.

If you are using C++ to implement the plug-in, you must ensure the methods are declared with C linkage to avoid [name mangling issues](http://en.wikipedia.org/wiki/Name_mangling).

```
extern "C" {
  float Foopluginmethod ();
}
```

After building the library, copy the output .so file(s) into the __Assets/Plugins/Android__ directory in your Unity project. In the Inspector, mark your .so files as compatible with Android, and set the required CPU architecture in the dropdown box:


![Native(C++) plug-in import settings as displayed in the Inspector window](../uploads/Main/AndroidNativePlugins.png)

                                                                                                                   
To call the methods in your native plug-in from within your C# scripts, use the following code:

```
[DllImport ("pluginName")]
private static extern float Foopluginmethod();
```

Note that pluginName should not include the prefix (‘lib’) or the extension (‘.so’) of the filename. It is recommended to wrap all the native plug-in method calls with an additional C# code layer. This code checks [Application.platform](https://docs.unity3d.com/ScriptReference/Application-platform.html) and calls native methods only when the app is running on the actual device; dummy values are returned from the C# code when running in the Editor. Use [platform defines](https://docs.unity3d.com/Manual/PlatformDependentCompilation.html) to control platform dependent code compilation.

##Native (C++) plug-in Sample
This [zip archive](https://docs.unity3d.com/uploads/Examples/AndroidNativePlugin.zip) contains a simple example of a native code plug-in.
This sample demonstrates how C++ code is invoked from a Unity application. The package includes a scene which displays the sum of two values as calculated by the native plug-in. You will need the [Android NDK)(https://developer.android.com/ndk/index.html)to compile the plug-in.

<br/>

----
* <span class="page-edit">2017-05-18  <!-- include IncludeTextNewPageNoEdit --></span>

* <span class="page-history">Updated features in 5.5</span>
