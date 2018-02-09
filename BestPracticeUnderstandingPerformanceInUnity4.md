# Asset auditing

Many of the problems found in real projects occur because of honest mistakes – temporary "test" changes and misclicks by a tired developer can silently add poorly-performing Assets, or change the import settings of existing Assets.

For any project of significant scale, it is best to have a first line of defense against human errors. It is relatively simple to write a small piece of code that ensures that no one can add a 4K uncompressed Texture to a project.

And yet, this is a surprisingly common problem. A 4K uncompressed Texture occupies 60 megabytes of memory. On a low-end mobile device, such as an iPhone 4S, it is dangerous to consume more than about 180-200 megabytes of memory. If added by mistake, this Texture inadvertently occupies between a third and a quarter of the application’s memory budget, and causes difficult-to-diagnose out-of-memory errors.

While it is now possible to track these issues down with the 5.3 Memory Profiler, it is arguably better to make sure such mistakes are impossible in the first place.

## Using AssetPostprocessor

The `AssetPostprocessor` class in the Unity Editor can be used to enforce certain minimum standards on a Unity project. This class receives callbacks when Assets are imported. To use it, inherit from `AssetPostprocessor` and implement one or more `OnPreprocess` methods. Significant ones include:

* `OnPreprocessTexture`

* `OnPreprocessModel`

* `OnPreprocessAnimation`

* `OnPreprocessAudio`

See the Scripting Reference on [AssetPostprocessor](ScriptRef:AssetPostprocessor.html) for more possible `OnPreprocess` methods.

```

public class ReadOnlyModelPostprocessor : AssetPostprocessor {

   public void OnPreprocessModel() {

        ModelImporter modelImporter =

 (ModelImporter)assetImporter;

        if(modelImporter.isReadable) {

            modelImporter.isReadable = false;

            modelImporter.SaveAndReimport();

        }

    }

}

```

This is a simple example of an `AssetPostprocessor` enforcing rules on a project:

This class is called any time a model is imported into the project, or whenever a model has its import settings changed. The code simply checks to see if the `Read/Write enabled` flag (represented by the `isReadable` property) is set to `true`. If it is, it forces the flag to be `false` and then saves and reimports the Asset.

Note that calling `SaveAndReimport` causes this snippet of code to be called again! However, because it is now assured that `isReadable` is false, this code does not produce an infinite reimport loop.

The reason for this change is discussed in the "Models" section, below.

##Common Asset rules

#### Textures

**Disable the read/write enabled flag**

The `Read/Write enabled` flag causes a Texture to be kept twice in memory: once on the GPU and once in CPU-addressable memory(1) (NOTE: 
	 This is because, on most platforms, readback from GPU memory is extremely slow. Reading a Texture from GPU memory into a temporary buffer for use by CPU code (e.g. Texture.GetPixel) would be very nonperformant.). In Unity, this setting is disabled by default, but it can be accidentally switched on.

`Read/Write Enabled` is only necessary when manipulating Texture data outside of Shaders (such as with the `Texture.GetPixel` and `Texture.SetPixel` APIs) and should be avoided whenever possible.

**Disable Mipmaps if possible**

For objects that have a relatively invariant Z-depth relative to the Camera, it is possible to disable mipmaps to save about a third of the memory required to load the Texture. If an object changes Z-depth, disabling mipmaps can lead to worse Texture sampling performance on the GPU.

In general, this is useful for UI Textures and other Textures that are displayed at a constant size on screen.

**Compress all Textures**

Using a texture compression format suitable for the project’s target platform is crucial for saving memory.

If the selected texture compression format is unsuited to the target platform, Unity decompresses the Texture when the Texture is loaded, consuming both CPU time and an excessive amount of memory. This is most commonly a problem on Android devices, which often support vastly different texture compression formats depending on the chipset.

**Enforce sensible Texture size limits**

While this is simple, it is also very easy to forget to resize a Texture or to inadvertently alter the Texture size import setting. Determine a sensible maximum size for different types of Textures and enforce these via code.

For many mobile applications, 2048x2048 or 1024x1024 is sufficient for Texture atlases, and 512x512 is sufficient for Textures applied to 3D models.

#### Models

**Disable the Read/Write enabled flag**

The`Read/Write enabled` flag for models operates identically to the one described for Textures. However, it is enabled by default for models.

Unity requires this flag to be enabled if a project is modifying a Mesh at runtime via script, or if the Mesh is used as the basis for a MeshCollider component. If the model is not used in a MeshCollider and is not manipulated by scripts, disable this flag to save half of the model’s memory.

**Disable rigs on non-character models**

By default, Unity imports a generic rig for non-character models. This causes an `Animator` component be to added if the model is instantiated at runtime. If the model is not animated via the Animation system, this adds unnecessary overhead to the animation system, because all active Animators must be ticked once per frame.

Disable the rig on non-animated models to avoid this automatic addition of an Animator component and possible inadvertent addition of unwanted Animators to a Scene.

**Enable the Optimize Game Objects option on animated models**

The __Optimize Game Objects__ option has a significant performance impact on animated models. When the option is disabled, Unity creates a large transform hierarchy mirroring the model’s bone structure whenever the model is instantiated. This transform hierarchy is expensive to update, especially if other components (such as Particle Systems or Colliders) are attached to it. It also limits Unity’s ability to multithread Mesh skinning and bone animation calculations.

If specific locations on a model’s bone structure need to be exposed (such as exposing a model’s hands in order to dynamically attach weapon models) then these locations can be specifically whitelisted in the `Extra Transforms` list.

Some additional details can be found in the Unity Manual page on the [Model Importer](https://docs.unity3d.com/Manual/FBXImporter-Rig.html).

**Use Mesh compression when possible**

Enabling Mesh compression reduces the number of bits used to represent the floating-point numbers for different channels of a model’s data. This can lead to a minor loss of precision, and the effects of this imprecision should be checked by artists before use in a final project.

The specific numbers of bits that a given compression level uses are detailed in the [ModelImporterMeshCompression](https://docs.unity3d.com/ScriptReference/ModelImporterMeshCompression.html) Scripting Reference.

Note that it is possible to use different levels of compression for different channels, so a project may choose to compress only tangents and normals while leaving UVs and vertex positions uncompressed.

**Note: Mesh Renderer Settings**

When adding Mesh Renderers to Prefabs or GameObjects, take note of the settings on the component. By default, Unity enables Shadow casting and receiving, Light Probe sampling, Reflection Probe sampling, and Motion Vector calculation.

If a project does not require one or more of these features, ensure that they’re turned off by an automated script. Any runtime code that adds MeshRenderers needs to toggle these settings as well.

For 2D games, accidentally adding a MeshRenderer to the Scene with the shadow options turned on adds a full shadow pass to the rendering loop. This is generally a waste of performance.

#### Audio

**Platform-appropriate compression settings**

Enable a compression format for audio that matches the available hardware. All iOS devices include hardware MP3 decompressors, and many Android devices support Vorbis natively.

Further, import uncompressed audio files into Unity. Unity always recompresses audio when building a project. There is no need to import compressed audio and then recompress it; this only serves to degrade the quality of the final audio clips.

**Force audio clips to mono**

Few mobile devices actually have stereo speakers. On a mobile project, forcing the imported audio clips to be mono-channel halves their memory consumption. This setting is also applicable to any audio without stereo effects, such as most UI sound effects.

**Reduce audio bitrate**

While this requires consultation with an audio designer, attempt to minimize the bitrate of audio files in order to further save on memory consumption and built project size.
