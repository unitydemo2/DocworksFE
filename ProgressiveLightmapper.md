# Progressive Lightmapper

## What

![](../uploads/Main/ProgressiveLightmapper-0.png)

The progressive lightmapper is a path tracing based lightmapper backend that provides baked lightmaps and light probes with progressive updates in the Editor.

The progressive lightmapper goes through a short prepare step (geometry and instance updates, G-buffer and chart mask generation) and starts producing the output very quickly. New lightmaps and light probes are shown as soon as a new intermediate result is ready. This allows for a very fast iteration workflow.

## Why

The old Enlighten-based lightmapper for baked lightmaps relied on precomputed realtime GI to generate indirect lighting. That was both an advantage, as just changing the lighting could produce new lightmaps fairly quickly, and a disadvantage, as it imposed all the UV layout limitations even for users only interested in baking. The UV requirements in the progressive lightmapper are the usual for baked lightmapping: non-overlapping UVs with small area and angle errors, and sensible padding between the charts.

The new lightmapper starts producing the output immediately and progressively refines it over time for a much improved lighting workflow - this means an interactive lighting workflow. Additionally, baking times are much more predictable.

See an in-depth video showing the interactive workflow [here](https://youtu.be/foMZJrwRGr0).

Moreover the new technique bakes global illumination at the lightmap resolution - for each texel individually - without upsampling schemes or relying on any irradiance caches or other global data structures. This makes it robust and allows you to bake selected portions of lightmaps, which means that iteration speed can be improved greatly.

## Setup

Newly created scenes have the progressive lightmapper enabled by default. Existing scenes will stick to Enlighten until you choose the "Progressive (experimental)" Bake Backend.

### Settings
![](../uploads/Main/ProgressiveLightmapper-2.png)

* __Bake Backend__ - "Enlighten" is the old baking backend and “Progressive (experimental)” is the new one.
* __Stationary Lighting Mode: __Specifies which scene lighting mode will be used for all stationary lights in the scene. Options are Baked Indirect, Distance Shadowmask, Shadowmask and Subtractive. Currently light modes are not supported, please be sure to set ‘Baked Indirect’ and do not use ‘Stationary’ lights. The support will come soon.
* __Lightmap Resolution__ - The amount of texels per world unit. Keep in mind that increasing this value by two, increases the amount of texels to be calculated by four. Please check the "Occupied texels" count in the stats below.
* __Lightmap Padding__ - The padding (in texels) between different instances in the atlas. In order to change padding between UV charts inside an instance please adjust ‘Pack Margin’ on the mesh importer in the Advanced settings under ‘Generate Lightmap UVs’.
* __Compress Lightmaps__ - Intermediate lightmaps are not compressed, but the final ones do respect the compression setting.
* __Samples__ - The amount of samples (paths) shot from each texel. For some scenes, especially outdoor scenes, 100 samples may be enough. For indoor scenes with emissive geometry more will be needed.
* __Bounces__ - Number of indirect bounces to do when tracing paths. For most scenes two bounces is enough. For some indoor scenarios more may be necessary.
* __Filtering__ - Configure the post-processing of lightmaps to limit noise. It can be set to None, Auto or Advanced. The Advanced option offers three additional parameters for manual configuration. In Auto mode the default values from the Advanced mode are used.
    * __Direct Radius: __The radius of the Gauss filter in texels for direct light in the lightmap. A higher radius will increase the blur strength.
    * __Indirect Radius: __The radius of the Gauss filter in texels for indirect light in the lightmap. A higher radius will increase the blur strength.
    * __AO Radius: __The radius of the Gauss filter in texels for ambient occlusion in the lightmap. A higher radius will increase the blur strength.
* __Prioritize View __- When enabled texels currently visible in scene view camera frustum will be prioritized. When those are done, the lightmapper will continue on all the out-of-view texels.

### Stats

The panel below the ‘Auto Generate’ and ‘Generate Lighting’ options shows the amount of lightmaps that were created, how many are in view (converged / not converged) and out of view (converged / not converged) and the bake performance.

![](../uploads/Main/ProgressiveLightmapper-3.png)

### Lightmap parameters

In addition to the Baked GI settings in the Lighting window, there are new parameters in the Lightmap Parameters asset that can be configured. These are Anti-aliasing Samples, Pushoff and Backface Tolerance. Default lightmap parameters can be set for the scene in *General GI > Default Parameters* or set per renderer.
![](../uploads/Main/ProgressiveLightmapper-4.png)

* __Anti-aliasing Samples __- The number of times to supersample a texel to reduce aliasing. Samples [1;3] disables supersampling, samples [4;8] give 2x supersampling, and samples [9;256] give 4x supersampling. (This is a bit weird UX-wise, we’ll improve on that front.) This mostly affects the amount of memory used for the positions and normals buffers (2x uses four times the amount of memory, 4x uses 16 times the amount of memory).
* __Pushoff __- The amount to push off ray origins away from geometry along the normal for ray tracing, in modelling units. It is applied to all baked lightmaps, so it affects direct light, indirect light and ambient occlusion. It is useful for getting rid of unwanted occlusion/shadowing.
* __Backface Tolerance __- The percentage of rays shot from an output texel that must hit front faces to be considered usable. Allows a texel to be invalidated if too many of the rays cast from it hit backfaces (the texel is inside some geometry). In that case artefacts are avoided by cloning valid values from surrounding texels. For example, if backface tolerance is 0.0, the texel is rejected only if it sees nothing but backfaces. If it is 1.0, the ray origin is rejected if it has even one ray that hits a backface. In the Baked Texel Validity scene view mode one case see valid (green) and invalid (red) texels. If you have a single sided mesh in your scene, you may want to disable this feature by setting it to zero. A two-sided flag will later be added in the editor to address this.

The rest is the default Unity 5 workflow. Mark your objects as static and set some light inputs (lights, environment lighting or emissive materials on static objects) as baked.

In "Auto" mode the lightmaps and light probes will be calculated automatically. If you have “Auto” disabled you will need to press the “Build” button for the bake to start.

### Other Features

__Force stop:__ Allows for stopping the bake at an arbitrary point in time, before the requested amount of samples has actually been done. It works when the lighting is built manually. With the 100,000 max sample count and the ability to disable view prioritization, one can leave the machine baking and just stop whenever the results look pleasing.![](../uploads/Main/ProgressiveLightmapper-5.jpg)

__Invalid texels:__ Texels are marked as invalid based on the Backface Tolerance parameter (LightmapParameters > General GI) and invalid texels are filled from the valid neighbours. The dilation process that takes care of that does more iterations once the lightmap has converged than when it’s still improving.

![](../uploads/Main/ProgressiveLightmapper-6.png)

__Supersampling:__ The lighting quality is influenced by the supersampling amount. Control it using the ‘Anti-aliasing Samples’ property (Lightmap Parameters > Baked GI, see the Lightmap Parameters section above).

## Example project

This [project](https://drive.google.com/open?id=0BwkcjTqCXtRNaEIxeG5Bdk9FV2M) is set up with the settings needed for the progressive lightmapper. It is a version of the [Tanks!](https://www.assetstore.unity3d.com/en/#!/content/46209) project also available on the Asset Store. It bakes in less than 5 minutes and has 11 1024x1024 lightmaps. Watch a [video](https://youtu.be/IsdH-uOLk2c) showing the interactive workflow in this project.

![](../uploads/Main/ProgressiveLightmapper-8.png)

![](../uploads/Main/ProgressiveLightmapper-9.png)

![](../uploads/Main/ProgressiveLightmapper-10.png)

![](../uploads/Main/ProgressiveLightmapper-11.png)

---

* <span class="page-edit">2017-07-04  <!-- include IncludeTextNewPageNoEdit --></span>

* <span class="page-history">2017-07-04 New feature in Unity 5.6 (Experimental)</span>
