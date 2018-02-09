PS Vita Stripping Levels
===

Setting a Stripping Level in the Player Settings can potentially reduce your game's memory footprint quite considerably. 

The available options are:

* Disabled (default)
* Strip Assemblies
* Strip ByteCode
* Use micro mscorlib

The size optimizations activated by stripping work in the following way:

1. **Strip assemblies level**: The scripts' bytecode is analyzed so that classes and methods that are not referenced from the scripts can be removed from the DLLs and thereby excluded from the AOT compilation phase. This optimization reduces the size of the main binary and accompanying DLLs and is safe as long as no reflection is used.

1. **Strip ByteCode level**: Any .NET DLLs (stored in the Data folder) are stripped down to metadata only. This is possible because all the code is already precompiled during the AOT phase and linked into the main binary.

1. **Use micro mscorlib level**: A special, smaller version of mscorlib is used. Some components are removed from this library, for example, Security, Reflection.Emit, Remoting, non Gregorian calendars, etc. Also, interdependencies between internal components are minimized. This optimization reduces the main binary and `mscorlib.dll` size but it is not compatible with some System and System.Xml assembly classes, so use it with care.

These levels are cumulative, so level 3 optimization implicitly includes levels 2 and 1, while level 2 optimization includes level 1.

Note that Micro mscorlib is a heavily stripped-down version of the core library. Only those items that are required by the Mono runtime in Unity remain. Best practice for using micro mscorlib is not to use any classes or other features of .NET that are not required by your application. GUIDs are a good example of something you could omit; they can easily be replaced with custom made pseudo GUIDs and doing this would result in better performance and app size.

##Tips
###How to Deal with Stripping when Using Reflection
Stripping depends highly on static code analysis and sometimes this can't be done effectively, especially when dynamic features like reflection are used. In such cases, it is necessary to give some hints as to which classes shouldn't be touched. Unity supports a per-project custom stripping blacklist. Using the blacklist is a simple matter of creating a link.xml file and placing it into the Assets folder. An example of the contents of the link.xml file follows. Classes marked for preservation will not be affected by stripping:-

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

### Simple Checklist for Making Your Distribution as Small as Possible

1. Minimize your assets: enable compression for textures and reduce their resolution as far as possible. Also, minimize the number of uncompressed sounds. 
1. Set the Vita Stripping Level to Use micro mscorlib.
1. Set the script call optimization level to Fast but no exceptions.
1. Don't use anything that lives in System.dll or System.Xml.dll in your code. These libraries are not compatible with micro mscorlib.
1. Remove unnecessary code dependencies.
1. Set the API Compatibility Level to .Net 2.0 subset. Note that .Net 2.0 subset has limited compatibility with other libraries.
1. Don't use JS Arrays.
1. Avoid generic containers in combination with value types, including structs.