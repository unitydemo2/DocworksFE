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

![](../uploads/Main/PlayerSetWebGLPub.png)

|**_Property:_** |**_Function:_** |
|:---|:---|
|__WebGL Memory Size__ |Sets the memory available to the WebGL runtime, given in megabytes. You should choose this value carefully: if it is too low, you will get out-of-memory errors because your loaded content and scenes won't fit into the available memory. However, if you request too much memory then some browser/platform combinations might not be able to provide it and consequently fail to load the player. See [here](webgl-memory) for details. |
|__Enable Exceptions__|Enable exception support |
|__Data caching__| Enable this to automatically cache your contents asset data on the users machine so it will not have to be re-downloaded on subsequent runs (unless the contents have changed). Caching is implemented using the IndexedDB API provided by the browser. Some browsers may implement restrictions around this, such as asking the user for permission to cache data over a specific size. |


Further information about WebGL Publishing Settings can be found in the [WebGL Building and Running](webgl-building) page.

