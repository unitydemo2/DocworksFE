#Optimizing the Size of the Built iOS Player

The two main ways of reducing the size of the player are by making proper __Release build__ within Xcode and by changing the __Stripping Level__ within Unity.


##Building for distribution

It is expected that final release builds are made using Xcode 4.x/5.x command __Product -&gt; Archive__. Using this command ensures that build is made with release configuration **and** all the debug symbols are stripped.
After issuing this command latest Xcode switches to Organizer window __Archives__ tab (you can navigate there manually via _Window -&gt; Organizer_ menu). You will find there two very useful functions there: __App Store size estimation__ and __Distribution__.
Build size estimation function works pretty well, but it is always recommended to have some small extra margin for error when aiming for 3G download limit (which currently is 100MB).



##iOS Stripping Level

The size optimizations activated by stripping work in the following way:


1. __Strip assemblies__ level: the scripts' bytecode is analyzed so that classes and methods that are not referenced from the scripts can be removed from the DLLs and thereby excluded from the AOT compilation phase. This optimization reduces the size of the main binary and accompanying DLLs and is safe as long as no reflection is used.


1. __Strip ByteCode__ level: any .NET DLLs (stored in the Data folder) are stripped down to metadata only. This is possible because all the code is already precompiled during the AOT phase and linked into the main binary.


1. __Use micro mscorlib__ level: a special, smaller version of mscorlib is used. Some components are removed from this library, for example, Security, Reflection.Emit, Remoting, non Gregorian calendars, etc. Also, interdependencies between internal components are minimized. This optimization reduces the main binary and mscorlib.dll size but it is not compatible with some System and System.Xml assembly classes, so use it with care.

These levels are cumulative, so level 3 optimization implicitly includes levels 2 and 1, while level 2 optimization includes level 1.

Note that __Micro mscorlib__ is a heavily stripped-down version of the core library. Only those items that are required by the Mono runtime in Unity remain. Best practice for using micro mscorlib is not to use any classes or other features of .NET that are not required by your application. GUIDs are a good example of something you could omit; they can easily be replaced with custom made pseudo GUIDs and doing this would result in better performance and app size. 

## Stripping with IL2CPP

The equivalent of __Strip ByteCode__ is always enabled when the IL2CPP scripting backend is used. In this case, the __Stripping Level__ option is replaced with an Boolean option named __Strip Engine Code__. If this option is enabled, unused modules and classes in the Unity Engine code will be removed, if it is disabled, all of the modules and classes in the Unity Engine code will be preserved.

The __link.xml__ file (described below) can be used to effectively disable byte code stripping by preserving both types and full assemblies. For example, to prevent the __System__ assembly from being stripped, the following link.xml file can be used:

````
<linker>
       <assembly fullname="System" preserve="all"/>
</linker>
````

**Note:** The ability to preserve an entire assembly applies only to the IL2CPP scripting backend.

##Tips

###How to Deal with Stripping when Using Reflection
Stripping depends highly on static code analysis and sometimes this can't be done effectively, especially when dynamic features like reflection are used. In such cases, it is necessary to give some hints as to which classes shouldn't be touched. Unity supports a per-project custom stripping _blacklist_. Using the blacklist is a simple matter of creating a __link.xml__ file and placing it into the __Assets__ folder (or any subdirectory of __Assets__). An example of the contents of the __link.xml__ file follows. Classes marked for preservation will not be affected by stripping:


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

	   <assembly fullname="mscorlib">
	           <type fullname="System.AppDomain" preserve="fields"/>
			   <type fullname="System.InvalidOperationException" preserve="fields">
			           <method signature="System.Void .ctor()"/>
               </type>
			   <type fullname="System.Object" preserve="nothing">
			          <method name="Finalize"/>
		       </type>
	   </assembly>
</linker>
````

A project can include multiple __link.xml__ files. Each __link.xml__ file can specify a number of different options.

* The __assembly__ element indicates the managed assembly where the nested directives should apply.
* The __type__ element is used to indicate how a specific type should be handled. It must be a child of the __assembly__ element. The __fullname__ attribute can accept the '*' wild card to match one or more characters.
  * The __preserve__ attribute can take on one of three values:
    * __all__: Keep everything from the given type (or assembly, for IL2CPP only).
    * __fields__: Keep only the fields of the given type.
    * __nothing__: Keep only the given type, bug none of its contents.
* The __method__ element is used to indicate that a specific method should be preserved. It must be a child of the __type__ element. The method can be specified by name or by signature.

The stripped assemblies are output to a directory below the __Temp__ directory in the project (the exact location varies depending on the target platform). The original, unstripped assemblies are available in the __not-stripped__ directory in the same location as the stripped assemblies. A tool like [ILSpy](http://ilspy.net/) can be used to inspect the stripped and unstripped assemblies to determine what parts of the code were removed.

**Note:** it can sometimes be difficult to determine which classes are getting stripped in error even though the application requires them. You can often get useful information about this by running the stripped application on the simulator and checking the Xcode console for error messages.

###Simple Checklist for Making Your Distribution as Small as Possible


1. Minimize your assets: enable PVRTC compression for textures and reduce their resolution as far as possible. Also, minimize the number of uncompressed sounds. There are some additional tips for file size reduction [here](ReducingFilesize).
1. Set the iOS Stripping Level to __Use micro mscorlib__.
1. Set the script call optimization level to __Fast but no exceptions__.
1. Don't use anything that lives in System.dll or System.Xml.dll in your code. These libraries are **not** compatible with micro mscorlib.
1. Remove unnecessary code dependencies.
1. Set the API Compatibility Level to __.Net 2.0 subset__. Note that .Net 2.0 subset has limited compatibility with other libraries.
1. Don't use JS Arrays.
1. Avoid generic containers in combination with value types, including structs.

###How small can an app be made with Unity?
An empty project would take less than 22 MB in the App Store if all the size optimizations were turned off. With code stripping, the empty scene with just the main camera can be reduced to less than 12 MB in the App Store (zipped and DRM attached). 

###Why did my app increase in size after being released to the App Store?
When publishing your app, Apple App Store service first encrypts the binary file and then compresses it via zip. Encryption increases ''randomness' of the code segment and thus makes it worse for compression. Check "Building for distribution" chapter above how to estimate App Store size before submission.
