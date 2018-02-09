New in 5.3
============

Each new release of Unity has many new features, improvements to existing features, changes, and fixes. This page is a quick guide to some of the main new or updated features in the manual. For a complete list, see the [Unity 5.3 release notes](https://unity3d.com/unity/whats-new/unity-5.3).

###Documentation for new features in 5.3:

**[Multi-Scene Editing](MultiSceneEditing)**: 
Open and edit multiple scenes at the same time. New features in the hierarchy window allow you to manage multiple scenes, so you can separate up your work into manageable individually-loadable chunks.


**[New 2D Joints](Joints2D), [Buoyancy Effector](class-BuoyancyEffector2D) & [Sprite Creator](SpriteCreator)**: 
New joint types have been added, plus a Buoyancy Effector allowing you to simulate a liquid volume, and a Sprite Creator, giving you "primitve"-style placeholders to use for working in 2D. 


**[OpenGL Core Support](OpenGLCoreDetails)**: 
OpenGL Core is the OpenGL equivalent of DirectX 11, and opens up many of the same advanced shader features on OpenGL platforms that DirectX 11 offers.

**[Euler Curve Animation Import](AnimationEulerCurveImport)**: 
By default, rotation curves are resampled as quaternions during import, however sometimes this can be undesirable and cause differences from your original animation. You can now choose to keep your rotation curves as Euler values.

**[LZ4 Asset Bundle Compression](AssetBundleCompression)**: 
A new compression option for asset bundles which allows partial decompression of only the required portion of the bundle. This avoids wait times which were previously incurred from having to decompress the entire bundle.

**[Sprite Flipping](class-SpriteRenderer)**: 
Flip sprites in the X or Y plane by checking a box, instead of needing to use negative transform scales.

**[Particle System Improvements](PartSysRotOverLifeModule)**: 
All properties now accessible via script! Also, new features such as [3D Rotation](PartSysRotOverLifeModule) & [Emission from Skinned Mesh surfaces](PartSysShapeModule). Lots of small updates too, so see the [5.3 release notes](https://unity3d.com/unity/whats-new/unity-5.3) for more info.

**[In-App Purchases](UnityIAP)**

Makes it easy to implement in-app Purchases in your Application across the most popular App stores, including iOS App Store, Mac App Store, Google Play and Windows Store.

**[Multi-Display support](MultiDisplay)**

Display up to 8 different camera views on 8 different monitors at the same time. Great for multi-display simulation rigs, public kiosk installations, etc.

**[Network Host Migration](UNetHostMigration)**

Allows one of the clients of a game to take over as the new host, if connection to the existing host is lost.

**[Asynchronous Texture Upload](AsyncTextureUpload)**

Enables time-sliced uploading of texture data to the GPU, which reduces wait time on the main game thread.

**[Speedtree Improvements](SpeedTree)**

Multi-core batching improvements now give better performance for billboard trees.

**[JSON Serialization](JSONSerialization)**

Allows you to easily convert from serializable Unity objects to JSON and back.


