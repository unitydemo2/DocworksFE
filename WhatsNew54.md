#New in Unity 5.4

Each new release of Unity has many new features, improvements, changes, and fixes. This page is a quick guide to the major new or updated features in the manual. For a complete list, see the [Unity 5.4 release notes](https://unity3d.com/unity/whats-new/unity-5.4.0).

If you are upgrading existing projects from an earlier version to 5.4, read the [Upgrade Guide to 5.4](UpgradeGuide54) for information about how your project may be affected.

###Documentation for new features in Unity 5.4:

**[Light Probe Proxy Volumes](class-LightProbeProxyVolume)**: 
Allows you to use more detailed information across the surface of large dynamic objects. Dynamic objects (which cannot use baked lightmaps) can now have different areas of the surface independently lit by different light probes within the bounding volume of the model.

**[GPU Instancing Support](GPUInstancing)**: 
A highly optimized method of drawing large numbers of identical models. Models which use the same material and mesh can be instanced on the GPU hardware, which incurs very few draw calls.

**[Texture Array Support](ScriptRef:Texture2DArray)**:
A feature introduced in Direct3D 10, OpenGL 3, OpenGL ES 3 and similar modern platforms. A Texture Array is a collection of 2D textures which all have the same size, format, which look like a single object to the GPU. They can be sampled in the shader with a texture element index. Using texture arrays can give a performance improvement over multiple individual textures.

**[Fast Graphics CopyTexture](ScriptRef:Graphics.CopyTexture)**:
A new fast way of copying texture information from one texture into another.

**[Particle Trigger Module](PartSysTriggersModule)**:
Particle systems now have the ability to trigger a Callback whenever they interact with one or more Trigger Colliders in the Scene. A Callback can be triggered when a particle enters or exits a Collider, or during the time a particle is inside or outside of the Collider. Particles also now have a [non-uniform scaling option](PartSysMainModule#scaling) allowing you to specify separate width and height values.