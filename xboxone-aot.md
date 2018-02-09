Xbox One: Ahead of Time Compiler
================================

For the Xbox One platform (as is the case of all consoles) all code must be compiled Ahead of Time (AOT).  Compared to Just In Time (JIT) AOT code has some specific limitations.  For example AOT can do absolutely no code generation and also has some limitation on the use of generic.  You can read an in-depth overview of limitations and workaround [here](http://developer.xamarin.com/guides/ios/advanced_topics/limitations/).

You should keep these limitations in mind when you are using code from the Asset Store.  Vendors may not have anticipated these limitations and their code may not compile or run on the Xbox One.  Some errors may not become apparent until your game runs and exercises the offending code path.  

Code Stripping
--------------


Setting a Stripping Level in the Player Settings can potentially reduce your game's memory footprint quite considerably. 

The available options are:

* Disabled (default)
* Strip Assemblies
* Stip ByteCode
* Use micro mscorlib

The size optimizations activated by stripping work in the following way:


1. **Strip assemblies level**: The scripts' bytecode is analyzed so that classes and methods that are not referenced from the scripts can be removed from the DLLs and thereby excluded from the AOT compilation phase. This optimization reduces the size of the main binary and accompanying DLLs and is safe as long as no reflection is used.


1. **Strip ByteCode level**: Any .NET DLLs (stored in the Data folder) are stripped down to metadata only. This is possible because all the code is already precompiled during the AOT phase and linked into the main binary.


1. **Use micro mscorlib level**: A special, smaller version of mscorlib is used. Some components are removed from this library, for example, Security, Reflection.Emit, Remoting, non Gregorian calendars, etc. Also, interdependencies between internal components are minimized. This optimization reduces the main binary and mscorlib.dll size but it is not compatible with some System and System.Xml assembly classes, so use it with care.

These levels are cumulative, so level 3 optimization implicitly includes levels 2 and 1, while level 2 optimization includes level 1.

Note that Micro mscorlib is a heavily stripped-down version of the core library. Only those items that are required by the Mono runtime in Unity remain. Best practice for using micro mscorlib is not to use any classes or other features of .NET that are not required by your application. GUIDs are a good example of something you could omit; they can easily be replaced with custom made pseudo GUIDs and doing this would result in better performance and app size.

Tips
----

###How to Deal with Overzealous Stripping
Stripping depends highly on static code analysis and sometimes this can remove code that is crucial to your game.  This can especially happen when dynamic features like reflection are used, or with callbacks which are not invoked in your game's scripts but are passed to and invoked by native code. In such cases, it is necessary to give some hints as to which classes shouldn't be touched. Unity supports a per-project custom stripping blacklist. Using the blacklist is a simple matter of creating a link.xml file and placing it into the Assets folder. An example of the contents of the link.xml file follows. Classes marked for preservation will not be affected by stripping:


````
<linker>
       <assembly fullname="System.Web.Services">
               <type fullname="System.Web.Services.Protocols.SoapTypeStubInfo" preserve="all"/>
               <type fullname="System.Web.Services.Configuration.WebServicesConfigurationSectionHandler" preserve="all"/>
       </assembly>

       <assembly fullname="System">
               <type fullname="System.Net.Configuration.WebRequestModuleHandler" preserve="all"/>
               <type fullname="System.Net.HttpRequestCreator" preserve="all"/>
               <type fullname="System.Net.FileWebRequestCreator" preserve="all"/>
       </assembly>
</linker>
````

Note: it can sometimes be difficult to determine which classes are getting stripped in error even though the application requires them. You will need to exercise your game's code paths that use generics and native callbacks to ensure the code is compiled properly.  Information will be sent to the log if a function was not compiled ahead of time as expected.