#Building and running a WebGL project

When you [build](PublishingBuilds) a WebGL project, Unity creates a folder with the following files:

* An _index.html_ file which browsers can navigate to load your content.

* A _TemplateData_ folder (when building with the default template) containing the build logo, loading bar and other template Assets. The build template folder is normally used to customize the appearance of the build while loading. See the User Manual page on [WebGL templates](webgl-templates) for more information.

* A _Build folder_ containing your generated build output files.

The _Build_ folder contains the following files (the _MyProject_ file name represents the name of your project).

* A _UnityLoader.js_ JavaScript file containing the code needed to load up the Unity content in the web page.

* A _MyProject.json_ JSON file containing all the necessary information about your build. The URL of this JSON file is provided as an argument for the Unity Loader when the build is instantiated. JSON file contains URLs of all the other build files, which can be absolute or relative to the location of the JSON file. JSON may contain additional Module parameters, such as the splash screen style or the initial size of the memory heap.

* A _MyProject.asm.framework.unityweb_ file containing the asm.js runtime and JavaScript plugins.

* A _MyProject.asm.code.unityweb_ file containing the asm.js module for your player.

* A _MyProject.asm.memory.unityweb_ file containing a binary image to initialize the heap memory for your player.

* A _MyProject.data.unityweb_ file containing the Asset data and Scenes.

The contents of the _*.unityweb_ files in the _Build_ folder may be compressed with gzip, brotli or may be uncompressed, depending on the Publishing Settings. See documentation on [deploying compressed builds](webgl-deploying) for more information

You can view your WebGL player directly in most browsers by opening the _index.html_ file. However, for security reasons, Chrome places restrictions on scripts opened from local file URLs, so this technique does not work in Chrome. To work round Chrome's restrictions, use Unity’s __Build & Run__ command ( __File__ > __Build & Run__); the file is then temporarily hosted in a local web server and opened from a local host URL. Alternatively, you can run Chrome with the `--allow-file-access-from-files` command line option which allows it to load content from local file URLs. This is required on a PC to allow execution of the build.

On some servers you need to explicitly make _.unityweb_ files accessible, because the server needs to provide these files to clients.

## Build player options

Access the WebGL options via the in the __Build Settings__ dialog box. (menu:  __File__ > __Build Settings...__). In the dialog box, select __WebGL__ from the __Platform__ list, then select __Player Settings…__.

![](../uploads/Main/WebGLBuilding-BuildPlayerOptions.png)

###Development Build

When you check the __Development Build__ checkbox, Unity generates a development build which has Profiler support and a development console to see errors. In addition, development builds do not compress content (that is, content is not [minified](https://en.wikipedia.org/wiki/Minification_%28programming%29)); they maintain JavaScript in human-readable form, preserving function names so you get useful stack traces for errors. Note, however, that this means development builds are very large, and too large to distribute.

###Use pre-built Engine

This option only appears when you have the __Development Build__ checkbox checked. Use the __Use pre-built Engine__ option in the Build Settings dialog box to speed up build iteration time during development. When this option is enabled, Unity rebuilds only the managed code and then links dynamically with the pre-build Unity engine, so the project is rebuilt approximately 30–40% faster. Note that this type of build is only suited for development purposes, as it always produces unstripped engine code. Due to the dynamic linking overhead, the performance of this type of build is slower than a normal build.

###Autoconnect Profiler

This option can only be enabled when you have the __Development Build__ checkbox checked. Check the __Autoconnect Profiler__ option to profile your Unity WebGL content. For WebGL, it is not possible to connect the [Profiler](ProfilerWindow) to a running build as on other platforms, so you have to use this option to connect the content to the Editor. This is because the Profiler connection is handled using WebSockets on WebGL, but a web browser only allows outgoing connections from the content.

##Player Settings

WebGL has some additional options in the __PlayerSettings__ Inspector window (menu: __Edit__ > __Project Settings__ > __Player__).

### Other Settings

![](../uploads/Main/WebGLBuilding-OtherSettings.png)


####Strip Engine Code

Open __Other Settings__ to access the __Strip Engine Code__  option. This option is checked by default to enable code stripping for WebGL. With this option checked, Unity does not include code for any classes you don’t use. For example, if you don’t use any physics components or functions, the whole physics engine is removed from your build. See the Stripping section below for more details.

### Publishing Settings

![](../uploads/Main/WebGLBuilding-PublishingSettings.png)

####WebGL Memory Size

Open __Publishing Settings__ to access the __WebGL Memory Size__ field. Here, you can specify how much memory (in MB) the content should allocate for its heap. If this value is too low, an “out of memory” error message appears. This means your loaded content and Scenes cannot fit into the available memory. However if this value too high, your content might fail to load in some browsers or on some machines, because the browser might not have enough available memory to allocate the requested heap size. This value is written to a property named `TOTAL_MEMORY` in the generated .json file, so if you want to experiment with this setting without having to rebuild your project, you can either edit the .json file or provide the updated `TOTAL_MEMORY` value as an additional WebGL instantiation parameter. See the User Manual page on [WebGL memory usage](webgl-memory) for more details.

####Enable Exceptions

Open __Publishing Settings__ to access __Enable Exceptions__. __Enable Exceptions__ allows you to specify how unexpected code behavior (generally considered errors) is handled at run time. It has these options:

* __None__: Select this if you don’t need any exception support. This gives the best performance and smallest builds. With this option, any exception thrown causes your content to stop with an error in that setting. 
* __Explicitly Thrown Exceptions Only__ (default): Select this to capture exceptions which are explicitly specified from a `throw` statement in your scripts and to also ensure `finally` blocks are called. Note that selecting this option makes the generated JavaScript code from your scripts longer and slower; This might only be an issue if scripts are the main bottleneck in your project.
* __Full Without Stacktrace__: Select this option to capture:
	* Exceptions which are explicitly specified from `throw` statements in your scripts (the same as in the _Explicitly Thrown Exceptions Only_ option)
	* Null References
	* Out of Bounds Array accesses
* __Full With Stacktrace__: This option is similar to the option above but it also captures Stack traces. Unity generates these exceptions by embedding checks for them in the code, so this option decreases performance and increases browser memory usage. Only use this for debugging, and always test in a 64-bit browser.

Select __Publishing Settings__ to access __Data Caching__.
Select this to enable automatic local caching of your player data. This option sets asset storage as a local cached in the browser’s IndexedDB database, so that assets won’t have to be downloaded again in subsequent runs of your content. Note that different browsers have different rules on allowing IndexedDB storage; browsers may ask the user for permission to store the data, and your build may exceed a size limit defined by the browser.

##Distribution size

When publishing for WebGL, it is important to keep your build size low so users get reasonable download times before the content starts. For generic tips on reducing asset sizes, see documentation on [Reducing the file size of the build](ReducingFilesize). 

###Hints and tips specific to WebGL

* Specify the __Crunch__ texture compression format for all your compressed textures in the [Texture Importer](class-TextureImporter).

* Don’t deploy development builds; they are not compressed or [minified](https://en.wikipedia.org/wiki/Minification_%28programming%29), and so have much larger file sizes.

* Go to __PlayerSettings__ (menu: __Edit__ > __Project Settings__ > __Player__), open __Publishing Settings__ and set __Enable Exceptions__ to __None__ if you don’t need exceptions in your build.

* Go to __PlayerSettings__ (menu: __Edit__ > __Project Settings__ > __Player__), open __Other Settings__ and enable __Strip Engine Code__ to ensure an efficient build.

* Take care when using third-party managed dlls, as they might include a lot of dependencies and so significantly increase the generated code size.

If you make a release build, Unity compresses the build output files according to the __Compression Format__ selected in the WebGL __PlayerSettings__ > __Publishing Settings__ window. 


![](../uploads/Main/WebGLBuilding-CompressionFormat.png)


See documentation on [Deploying compressed builds](webgl-deploying) for more info on these options, and on how to publish builds with them.

##AssetBundles

Since all your Asset data needs to be pre-downloaded before your content starts, you should consider moving Assets out of your main data files and into [AssetBundles](AssetBundlesIntro). That way, you can create a small loader Scene for your content which loads quickly. It then dynamically loads Assets on-demand as the user proceeds through your content. AssetBundles also help with [Asset data memory](webgl-memory) management: You can unload Asset data from memory for Assets you don’t need any more by calling [AssetBundle.Unload](ScriptRef:AssetBundle.Unload.html).

Some considerations apply when using AssetBundles on the WebGL platform:

* When you use class types in your AssetBundle which are not used in your main build, Unity may strip the code for those classes from the build. This can cause a fail when trying to load Assets from the AssetBundle. Use [BuildPlayerOptions.assetBundleManifestPath](ScriptRef:BuildPlayerOptions-assetBundleManifestPath.html) to fix that, or see the section on _[Stripping](#Stripping)_, below, for other options.

* WebGL does not support threading, but http downloads only become available when they have finished downloading. Because of this, Unity WebGL builds need to decompress AssetBundle data on the main thread when the download is done, blocking the main thread. To avoid this interruption, [LZMA AssetBundle compression](AssetBundles-Building) is not available for AssetBundles on WebGL. AssetBundles are compressed using LZ4 instead, which is de-compressed very efficiently on-demand. If you need smaller compression sizes than LZ4 delivers, you can configure your web server to use gzip or Brotli compression (on top of LZ4 compression) on your AssetBundles. See documentation on [Deploying compressed builds](webgl-deploying) for more information on how to do this.

* AssetBundle caching using [WWW.LoadFromCacheOrDownload](ScriptRef:WWW.LoadFromCacheOrDownload.html) is supported in WebGL using the IndexedDB API from the browser to implement caching on the user’s computer. Note that IndexedDB may have limited support on some browsers, and that browsers may request the user’s authorization to store data on disk. See documentation on [WebGL browser compatibility](webgl-browsercompatibility) for more information.

<a name="Stripping"></a>
## **Stripping**

Unity removes all unused code from your build by default. You can change this via the __PlayerSettings__ Inspector window (menu: __Edit__ > __Project Settings__ > __Player__): Select __Other Settings__ to access the __Strip Engine Code__  option.  It is better to build with stripping enabled.

With code stripping, Unity scans your project for any `UnityObject`-derived classes used (either by being referenced in your script code, or in the serialized data in your Scenes). It then removes from the build any Unity subsystems which have none of their classes used. This makes your build have less code, resulting in both smaller downloads and less code to parse (so code runs faster and uses less memory).

## Issues with code stripping

Code stripping might cause issues with your project if it strips code which is actually necessary. This can be the case when you load AssetBundles at run time which contain classes that are not included in the main build, and have therefore been stripped from the project. Error messages appear in your browser’s JavaScript console when this happens (possibly followed by more errors). For example:

`Could not produce class with ID XXX`

To troubleshoot these errors, look up the ID (such as `XXX` in the example above) in the [Class ID Reference](ClassIDReference) to see which class it is trying to create an instance of. In such cases, you can force Unity to include the code for that class in the build, either by adding a reference to that class to your scripts or to your Scenes, or by adding a _link.xml_ file to your project. 

Below is an example which makes sure that the Collider class (and therefore the Physics module) gets preserved in a project. Add this XML code to a file called _link.xml_, and put that file into your _Assets_ folder.

````
<linker>
    <assembly fullname="UnityEngine">
        <type fullname="UnityEngine.Collider" preserve="all"/>
    </assembly>
</linker>

````

If you suspect that stripping is causing problems with your build, you can also try disabling the __Strip Engine Code__ option during testing. 

Unity does not provide a convenient way to see which modules and classes are included in a build, which would allow you to optimize your project to strip well. However, to get an overview of included classes and modules, you can look at the generated file _Temp/StagingArea/Data/il2cppOutput/UnityClassRegistration.cpp_ after making a build.

Note that the  __Strip Engine Code__ option only affects Unity engine code. IL2CPP always strips byte code from your managed dlls and scripts. This can cause problems when you need to reference managed types dynamically through reflection rather than through static references in your code. If you need to access types through reflection, you may also need to set up a _link.xml_ file to preserve those types. See the documentation page on [iOS Build size optimization](iphone-playerSizeOptimization) for more information on _link.xml_ files.

##Moving build output files

To change the location of your _Build_ folder, change the URL of the JSON file (the second argument of the _UnityLoader.instantiate_) in the index.html file. 

To change the location of the files inside the Build folder, change their URLs (that is, _dataUrl_, _asmCodeUrl_, _asmMemoryUrl_, and _asmFrameworkUrl_) in the JSON file. All non-absolute URLs in the JSON file are treated as URLs relative to the location of the JSON file. You can specify URLs on external servers for these if you want to host your files on a content distribution network (CDN), but you need to make sure that the hosting server has enabled Cross Origin Resource Sharing (CORS) for this to work. See the manual page on [WebGL networking](webgl-networking) for more information about CORS.

##Incremental builds

The C++ code generated for your project by IL2CPP is compiled incrementally; that is, only generated C++ code that has changed since the last build is compiled again. Unchanged source code re-uses the same object files generated for the previous build. The object files used for incremental C++ builds are stored in the _Library/il2cpp_cache_ directory in your Unity project. 

To perform a clean, from-scratch build of the generated C++ code which doesn’t use incremental compiling,  delete the _Library/il2cpp_cache_ directory in your Unity project. Note that if the Unity Editor version differs from the one used for the previous WebGL build, Unity does a clean, from-scratch build automatically.

---

* <span class="page-edit">2017-08-25  <!-- include IncludeTextAmendPageSomeEdit --></span>

* <span class="page-history">Full Without Stacktrace added in Unity 2017.3</span>