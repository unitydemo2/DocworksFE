# Building AssetBundles

In the documentation on the [AssetBundle Workflow](#AssetBundles-Workflow), we have a code sample which passes three arguments to the `BuildPipeline.BuildAssetBundles` function. Let’s dive a little deeper into what we’re actually saying.

_Assets/AssetBundles_: This is the directory that the AssetBundles will be output to. You can change this to any output directory you desire, just ensure that the folder actually exists before you attempt a build.

#### BuildAssetBundleOptions

There are several different `BuildAssetBundleOptions` that you can specify that have a variety of effects. See Scripting API Reference on [BuildAssetBundleOptions](ScriptRef:BuildAssetBundleOptions.html) for a table of all the options.

While you’re free to combine `BuildAssetBundleOptions` as needs change and arise, there are three specific `BuildAssetBundleOptions` that deal with AssetBundle Compression:

* `BuildAssetBundleOptions.None`: This bundle option uses LZMA Format compression, which is a single compressed LZMA stream of serialized data files. LZMA compression requires that the entire bundle is decompressed before it’s used. This results in the smallest possible file size but a slightly longer load time due to the decompression. It is worth noting that when using this BuildAssetBundleOptions, in order to use any assets from the bundle the entire bundle must be uncompressed initially. <br/> Once the bundle has been decompressed, it will be recompressed on disk using LZ4 compression which doesn’t require the entire bundle be decompressed before using assets from the bundle. This is best used when a bundle contains assets such that to use one asset from the bundle would mean all assets are going to be loaded. Packaging all assets for a character or scene are some examples of bundles that might use this. <br/> Using LZMA compression is only recommended for the initial download of an AssetBundle from an off-site host due to the smaller file size. Once the file has been downloaded, it will be cached as a LZ4 compressed bundle.

* `BuildAssetBundleOptions.UncompressedAssetBundle`: This bundle option builds the bundles in such a way that the data is completely uncompressed. The downside to being uncompressed is the larger file download size. However, the load times once downloaded will be much faster.

* `BuildAssetBundleOptions.ChunkBasedCompression`: This bundle option uses a compression method known as LZ4, which results in larger compressed file sizes than LZMA but does not require that entire bundle is decompressed, unlike LZMA, before it can be used. LZ4 uses a chunk based algorithm which allows the AssetBundle be loaded in pieces or "chunks." Decompressing a single chunk allows the contained assets to be used even if the other chunks of the AssetBundle are not decompressed.

Using `ChunkBasedCompression` has comparable loading times to uncompressed bundles with the added benefit of reduced size on disk.

#### BuildTarget

`BuildTarget.Standalone`: Here we’re telling the build pipeline which target platform we are going to be using these AssetBundles for. You can find a list of the available explicit build targets in the Scripting API Reference for [BuildTarget](ScriptRef:BuildTarget.html). However, if you’d rather not hardcode in your build target, feel free to take advantage of `EditorUserBuildSettings.activeBuildTarget` which will automatically find the platform you’re currently setup to build for and build your AssetBundles based on that target.

Once you’ve properly set up your build script, it’s finally time to build your bundles. If you followed the script example above, click __Assets__ > __Build AssetBundles__ to kick off the process.

Now that you’ve successfully built your AssetBundles, you may notice that your AssetBundles directory has more files than you might have originally expected. 2*(n+1) more files, to be exact. Let’s take a minute and go over exactly what the `BuildPipeline.BuildAssetBundles` yields.

For every AssetBundle you specified in the editor, you’ll notice a file with your AssetBundle name and your AssetBundle name + ".manifest".

There will be an additional bundle and manifest that doesn’t share a name with any AssetBundle you created. It, instead, is named after the directory that it’s located in (where the AssetBundles were built to). This is the Manifest Bundle. We’ll discuss more about this and how to use it in the future.

#### The AssetBundle File

This is the file that lacks the .manifest extension and what you’ll be loading in at runtime in order to load your Assets.

The AssetBundle file is an archive that contains multiple files internally. The structure of this archive can change slightly depending on if it is an AssetBundle or a Scene AssetBundle. This is the structure of a normal AssetBundle:

![](../uploads/Main/AssetBundles-Building-0.png)

The Scene AssetBundle changes from normal AssetBundles in that it is optimized for stream loading of a Scene and its content. This image shows the internal structure of the scene bundle:

#### The Manifest File

For every bundle generated, including the additional Manifest Bundle, an associated manifest file is generated. The manifest file can be opened with any text editor and contains information such as the cyclic redundancy check (CRC) data and dependency data for the bundle. For the normal AssetBundles their manifest file will look something like this:

```
ManifestFileVersion: 0
CRC: 2422268106
Hashes:
  AssetFileHash:
    serializedVersion: 2
    Hash: 8b6db55a2344f068cf8a9be0a662ba15
  TypeTreeHash:
    serializedVersion: 2
    Hash: 37ad974993dbaa77485dd2a0c38f347a
HashAppended: 0
ClassTypes:
- Class: 91
  Script: {instanceID: 0}
Assets:
  Asset_0: Assets/Mecanim/StateMachine.controller
Dependencies: {}

Which shows the contained assets, dependencies, and other information.

The Manifest Bundle that was generated will have a manifest, but it’ll look more like this:

ManifestFileVersion: 0
AssetBundleManifest:
  AssetBundleInfos:
    Info_0:
      Name: scene1assetbundle
      Dependencies: {}
```

This will show how AssetBundles relate and what their dependencies are. For now, just understand that this bundle contains the AssetBundleManifest object which will be incredibly useful for figuring out which bundle dependencies to load at runtime. To learn more about how to use this bundle and the manifest object, see documentation on [Using AssetBundles Natively](#AssetBundles-Native).

---

<span class="page-edit">• 2017-05-15  <!-- include IncludeTextNewPageNoEdit --></span><br/>
