# AssetBundles

An __AssetBundle__ is an archive file containing platform specific Assets (Models, Textures, Prefabs, Audio clips, and even entire Scenes) that can be loaded at runtime. AssetBundles can express dependencies between each other; e.g. a material in AssetBundle A can reference a texture in AssetBundle B. For efficient delivery over networks, AssetBundles can be compressed with a choice of built-in algorithms depending on use case requirements (LZMA and LZ4).

AssetBundles can be useful for downloadable content (DLC), reducing initial install size, loading assets optimized for the end-user’s platform, and reduce runtime memory pressure.

## What’s in an AssetBundle?

Good question, actually "AssetBundle" can refer to two different, but related things. 

First is the actual file on disk. This we call the AssetBundle archive, or just archive for short in this document. The archive can be thought of as a container, like a folder, that holds additional files inside of it. These additional files consist of two types; the serialized file and resource files. The serialized file contains your assets broken out into their individual objects and written out to this single file. The resource files are just chunks of binary data stored separately for certain assets (textures and audio) to allow us to load them from disk on another thread efficiently.

Second is the actual AssetBundle object you interact with via code to load assets from a specific archive. This object contains a map of all the file paths of the assets you added to this archive to the objects that belong to that asset that need to be loaded when you ask for it.

## Pages in this section

* [AssetBundle Workflow](#AssetBundles-Workflow)
* [Preparing Assets for AssetBundles](#AssetBundles-Preparing)
* [Building AssetBundles](#AssetBundles-Building)
* [AssetBundle Dependencies](#AssetBundles-Dependencies)
* [Using AssetBundles Natively](#AssetBundles-Native)
* [AssetBundle Manager](#AssetBundles-Manager)
* [Patching with AssetBundles](#AssetBundles-Patching)
* [Troubleshooting](#AssetBundles-Troubleshooting)

<br/>

----

* <span class="page-edit">2017-05-15  <!-- include IncludeTextNewPageNoEdit --></span>
