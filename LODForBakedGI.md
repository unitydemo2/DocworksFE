# LOD for baked lightmaps

Direct lighting is computed using the actual geometric surfaces of all levels of detail ([LODs](LevelOfDetail)). Lower LOD levels use Light Probes to sample indirect lighting.

The Unity Editor bakes the final lighting into [lightmaps](LightingInUnity) - the baked LODs do not sample the [Light Probes](LightProbes) at runtime if you use [baked GI](LightingGiUvs). To ensure you capture indirect lighting, place Light Probes around your baked LODs.

To set up LOD for baked lightmaps:

* Add a LOD Group (see documentation on [LOD](LevelOfDetail) for instructions on how to do this).
* Make the LOD GameObjects __Lightmap Static__  in the [Inspector](UsingTheInspector) (Inspector window: __Static__ > __Lightmap Static__) (see documentation on [Static Objects](StaticObjects) for more information).
* Place [Light Probes](LightProbes) around the LOD GameObjects.

Please note that only `LOD0` affects the surrounding geometry. However, the lower LODs are usually the same size as `LOD0`, so this should not cause any problems with your project.

The Unity Editor does not support LOD for precomputed realtime GI - it uses Light Probes instead.