# Procedural Materials - Memory Usage and Caching Behaviour

Substance (the Procedural Materials engine in Unity) makes use of two forms of caching, and to manage memory and disk usage when using procedural materials it is important to understand how they both behave.

## 1) The 'runtime' memory cache

Susbtance allows you to generate dynamic textures (textures that can obey a set of parameters) from a small amount of data. However, in order to generate the textures from the binary data and the parameter values, Substance needs to allocate some memory to store intermediate bitmaps when 'recompositing' the desired output textures.

The amount of memory Substance is allowed to use during the texture generation is controlled by [ProceduralMaterial.cacheSize](ScriptRef:ProceduralMaterial-cacheSize).

Once a Procedural Material's textures have been generated, and according to the current value of cacheSize, the Substance engine can keep some of the intermediate results in memory, in order to speed up subsequent texture computations if the user changes the value of one or several parameters later on.

Once this is done, [ProceduralMaterial.ClearCache()](ScriptRef:ProceduralMaterial.ClearCache) forces the Substance engine to release the memory it kept allocated, and to release the storage used to store the data of the input bitmaps if any.

So, the quickest way to lower the memory consumption of the Substance engine once the textures have been computed is as follows:

````
procMat.cacheSize = ProceduralCacheSize.None;
procMat.ClearCache();
````

*This function can be called per-material, and it's safe to think of it as such. However under the hood, Substance may optimize space by reusing shared parts of materials (for example if a basic noise pattern is used by two different materials). In addition, depending on the order in which assets are serialized during the build process and loaded at runtime, or even on the performance of the machine the game/app runs on, the merging of assets is not deterministic. Therefore if you are trying to closely track the amount of memory used by each material, this information may help explain if you are seeing unpredictable results.*


## 2) The on-device disk/flash cache

In order not to pay the texture generation time each time the game/app starts, it is possible to set up the Procedural Material in the editor to use a caching load behaviour.

![The Load Behaviour options in the inspector for a Substance material](../uploads/Main/SubstanceLoadBehaviour.png)

This option gives you control over when the textures are generated for the first time (either once the asset is loaded for the first time, or the first time the user triggers the texture computation via a script call), how the generated texures are cached, and whether the substance data is kept in memory to allow modification and regeneration at runtime.

The options available are:

Option Name | Description
--|--
Do nothing|Do not generate the textures. RebuildTextures() or RebuildTexturesImmediately() must be called to generate the textures.
Do nothing and cache|Do not generate the textures. RebuildTextures() or RebuildTexturesImmediately() must be called to generate the textures. After the textures have been generrated for the first time, they are cached to disk/flash to speed up subsequent game/application startups.
Build on level load|Generate the textures when loading to favor application's size (default on supported platforms).
Build on level load and cache|Generate the textures when loading and cache them to disk/flash to speed up subsequent game/application startups.
Bake and keep Substance|Bake the textures to speed up loading and keep the Procedural Material data so that it can still be tweaked and regenerated later on.
Bake and discard Substance|Bake the textures to speed up loading and discard the Procedural Material data (default on unsupported platforms).

When the generated textures are cached on-device, the next time the game/app cold starts, the textures are directly loaded from disk, and this is almost as fast as loading regular bitmaps. This means no time is spent generating textures at all, except for the first time the app is run.

## Clearing cached data

The cached data can be cleared using [Caching.ClearCache()](ScriptRef:Caching.ClearCache). This is the same cache space as is used for any download assetbundle data, so calling `ClearCache` will clear cached Procedural Material data *and* downloaded Asset Bundle data.

