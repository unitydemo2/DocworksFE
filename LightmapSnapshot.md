# Lighting Data Asset

Lightmap Snapshot was renamed to Lighting Data Asset in Unity 5.3.

You generate the Lighting Data Asset by pressing the Build button in the Lighting window. Your lighting will be loaded from that asset when you reload the scene.

The Lighting Data Asset contains the GI data and all the supporting files needed when creating the lighting for a scene. The asset references the renderers, the realtime lightmaps, the baked lightmaps, light probes, reflection probes and some additional data that describes how they fit together. This also includes all the Enlighten data needed to update the realtime global illumination in the Player. The asset is an Editor only construct so far, so you can't access it in the player.
When you change the scene, for instance by breaking a prefab connection on a lightmap static object, the asset data will get out of date and has to be rebuilt.

Currently, this file is a bit bloated as it contains data for multiple platforms - we will fix this. Also we are considering adding some compression for this data.

The intermediate files that are generated during the lighting build process, but is not needed for generating a Player build is not part of the asset, they are stored in the [GI Cache](GICache) instead.

The build time for the Lighting Data Asset can vary. If your [GI Cache](GICache) is fully populated i.e. you have done a bake on the machine before (with the scene in its current state) it will be fast. If you are pulling the scene to a machine with a blank cache or the cache data needed has been removed due to the cache size limit, the cache will have to be populated with the intermediate files first which requires the precompute and bake processes to run. These steps can take some time.