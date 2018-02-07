#WebGL Player Settings

This page details the __Player Settings__ specific to WebGL. A description of the general Player Settings can be found [here](class-PlayerSettings).

##Other settings

![](../uploads/Main/PlayerSetWebGLOther.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|**Rendering** ||
|__Rendering Path__ |The [rendering path](RenderingPaths) enabled for the game. |
|__Auto Graphics API__ |Uncheck this if you want to manually select which graphics API is used. When checked, Unity includes WebGL2.0, with WebGL1.0 as a fallback for browsers that don't support it. When unchecked, you can manually pick and reorder the graphics APIs. |
|__Static Batching__ |Check to enable static batching? |
|__Dynamic Batching__ |Check to enable dynamic batching. |
|**Configuration** ||
|__Scripting Backend__| Scripting backend is grayed out because there is only one scripting backend on WebGL. |
|__Disable HW Statistics__ |When this is unchecked, the application sends information about the hardware to Unity (See [hwstats](http://hwstats.unity3d.com/) page for more details).|
|__Scripting Define Symbols__|Custom compilation flags (see the [platform dependent compilation](PlatformDependentCompilation) page for details).|
|**Optimization** ||
|__Api Compatibility Level__ |Specifies active .NET API profile. See below.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__.Net 2.0__ |.Net 2.0 libraries. Maximum .net compatibility, biggest file sizes|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__.Net 2.0 Subset__ |Subset of full .net compatibility, smaller file sizes|
|__Prebake Collision Meshes__ |Enable collision mesh baking during the build. |
|__Preload Shaders__ |Enable shader preloading. |
|__Preload Assets__ |Enable asset preloading. Specify the size of assets to preload.|
|__Strip Engine Code__ |Enable code stripping for WebGL. |
|__Vertex Compression__ | |
|__Optimize Mesh Data__|Remove any data from meshes that is not required by the material applied to them (tangents, normals, colors, UV).|


###API compatibility level

You can choose your mono API compatibility level for all targets. Sometimes a 3rd party .net dll will use things that are outside of the .net compatibility level that you would like to use. In order to understand what is going on in such cases, and how to best fix it, get "Reflector" on windows. 

1. Drag the .net assemblies for the API compatilibity level in question into reflector. You can find these in Frameworks/Mono/lib/mono/YOURSUBSET/
1. Also drag in your third-party assembly.
1. Right click your third-party assembly, and select __Analyze__.
1. In the analysis report, inspect the __Depends on__ section. Anything that the third-party assembly depends on, but is not available in the .net compatibility level of your choice, will be highlighted in red there.


##Publishing settings

![](../uploads/Main/WebGLBuilding-PublishingSettings.png)

|**_Property:_** |**_Function:_** |
|:---|:---|
|__WebGL Memory Size__ |Sets the memory available to the WebGL runtime, given in megabytes. You should choose this value carefully: if it is too low, you will get out-of-memory errors because your loaded content and scenes won't fit into the available memory. However, if you request too much memory then some browser/platform combinations might not be able to provide it and consequently fail to load the player. See [here](webgl-memory) for details. |
|__Enable Exceptions__|Enables exceptions support which allows you to specify how unexpected code behavior (generally considered errors) is handled at run time. There are four options: None, Explicitly Thrown Exceptions Only, Full Without Stacktrace and Full With Stacktrace. See the [Building and running a WebGL project](webgl-building) page for details. |
|__Compression Format__|Release build files compression format: gzip, brotli or none. Note that this option does not affect Development builds. |
|__Name Files As Hashes__|Use MD5 hash of the uncompressed file contents as a filename for each file in the build.|
|__Data caching__|Enable this to automatically cache your contents asset data on the users machine so it will not have to be re-downloaded on subsequent runs (unless the contents have changed). Caching is implemented using the IndexedDB API provided by the browser. Some browsers may implement restrictions around this, such as asking the user for permission to cache data over a specific size.|
|__Debug Symbols__|Preserve debug symbols and perform demangling of the stack trace when an error occurs. For release builds all the debug information is stored in a separate file which is downloaded from the server on demand when an error occurs. Development builds always have demangling support embedded in the main module and therefore are not affected by this option.|
|__WebAssembly (Experimental)__|If enabled, WebAssembly build files are generated during a build. At run-time, if supported by the browser WebAssembly is used, otherwise it falls back to asm.js.|

Further information about WebGL Publishing Settings can be found in the [WebGL Building and Running](webgl-building) page.

---

* <span class="page-edit">2017-08-25  <!-- include IncludeTextAmendPageNoEdit --></span>

* <span class="page-history">Publishing settings updated in Unity [2017.3](https://docs.unity3d.com/2017.3/Documentation/Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20173</span></span>