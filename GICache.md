# GI cache

The GI cache is used by the Global Illumination (GI) system to store intermediate files when precomputing real-time GI, and when baking Static Lightmaps, Light Probes and Reflection Probes. The cache is shared between all Unity projects on the computer, so projects with the same content and same version of the lighting system (Enlighten) can share the files and speed up subsequent builds.

Find the settings for the GI cache in __Edit__ > __Preferences__ > __GI Cache__ on Windows, or __Unity__ > __Preferences__ > __GI Cache__ on macOS.

![](../uploads/Main/GICache.png)

|**Property:** |**Function:** |
|:---|:---|
| __Maximum Cache Size (GB)__ | Use the slider to define the maximum size of the GI cache, in gigabytes. When the GI cache's size grows larger than the size specified in __Preferences__ > __GI Cache__, Unity spawns a job to trim the cache. The trim job removes some files so the GI cache does not exceed the size specified. It removes files based on when they were last accessed; it removes those which were last accessed the longest time ago, and keeps those that were most recently used. <br/>**Note**: If all the files in the GI cache are currently being used by the current Scene (perhaps because the Scene is very large or the cache size is set too low), increase your cache size. Otherwise, resource-intensive recomputation occurs when baking. |
| __Custom cache location__ | By default, the GI cache is stored in the _Caches_ folder. Tick __Custom cache location__ to override the default location and set your own. <br/>**Note**: Storing the GI Cache on an SSD drive can speed up baking in cases where the baking process is I/O bound. |
| __Cache compression__ | Tick this checkbox to allow Unity to compress files in the GI cache. The files are LZ4 compressed by default, and the naming scheme is a hash and a file extension. The hashes are computed based on the inputs to the lighting system, so changing any of the following can lead to recomputation of lighting:<br/>- Materials (Textures, Albedo, Emission)<br/>- Lights<br/>- Geometry<br/>- Static flags<br/>- Light Probe groups<br/>- Reflection probes<br/>- Lightmap Parameters |
| __Clean Cache__ | Use the __Clean Cache__ button to delete the GI Cache directory. <br/>It is not safe to delete the GI Cache directory manually while the Editor is running. This is because the _GiCache_ folder is created on Editor startup, and the Editor maintains a collection of hashes that are used to look up the files in the _GiCache_ folder. If a file or directory suddenly disappears, the system can’t always recover from the failure, and prints an error in the Console. The __Clean Cache__ button ensures that the Editor releases all references to the files on disk before they are deleted. |

## GI cache and lighting

* To ensure that the the lighting data loads from the GI cache in a very short amount of time when you reload your Scene, open the Lighting window (menu: __Window__ > __Lighting__) and tick the __Auto__ checkbox next to the build button. This makes lightmap baking automatic, meaning that the lightmap data is stored in the GI cache.

* In the Lighting window, you can clear the baked data in a Scene (untick the __Auto__ checkbox, click the __Build__ button drop-down and select __Clear Baked Data__). This does not clear the GI Cache, because this would increase bake time afterwards.

* You can share the _GiCache_ folder among different machines. This can make your lighting build faster, because the files are downloaded from the _GiCache_ folder instead of computed locally. Note that the build process isn’t optimized for slow network-attached storage (NAS), so test if your bake times are severely affected before moving the cache to NAS.