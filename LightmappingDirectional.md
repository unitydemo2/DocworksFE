# Lightmap Directional Modes

There are two __Directional Modes__ available for light maps: __Directional__ and __Non-Directional__. To set the __Directional Mode__ for a light map, open the Lighting window (__Window__ > __Lighting__ > __Settings__), click __Scene__, navigate to the __Lightmapping Settings__, ensure the __Lightmapper__ is set to __Enlighten__, and use the __Directional Mode__ drop-down menu. Both are available as real-time and baked lightmaps.

__Directional__ light maps store more information about the lighting environment than __Non-Directional__ light maps. Shaders can use that extra data about incoming light to better calculate outgoing light, which is how materials appear on the screen. This happens at the cost of increased texture memory usage and shading time.

__Non-directional__: flat diffuse. This mode uses just a single lightmap, storing information about how much light does the surface emit, assuming it’s purely diffuse. Objects lit this way will appear flat (normalmaps won’t be used) and diffuse (even if the material is specular), but otherwise will be lit correctly. These barrels are using baked lightmaps. The only detail definition comes from a reflection probe and an occlusion map.

![](../uploads/Main/DirectionalLightmapping1.png) 

__Directional__: normal mapped diffuse. This mode adds a secondary lightmap, which stores the incoming dominant light direction and a factor proportional to how much light in the first lightmap is the result of light coming in along the dominant direction. The rest is then assumed to come uniformly from the entire hemisphere. That information allows the material to be normal mapped, but it will still appear purely diffuse.

![](../uploads/Main/DirectionalLightmapping2.png) 

## Performance

__Directional__ mode uses twice as much texture memory as __Non-directional__ mode and has a slightly higher shading cost. 

* __Non-directional:__ one texture, one texture sample, a few extra shader instructions. 

* __Directional:__ two textures, two texture samples, a few more extra shader instructions. 

Real-time lightmaps take advantage of the same approach, and are subject to the same shading quality/cost tradeoffs. 

The BRDF that is actually used for indirect light (the indirect part of baked) is a slightly less expensive version. `UNITY_BRDF_PBS_LIGHTMAP_INDIRECT` is defined in *UnityPBSLighting.cginc*.

## Specular lighting on light maps

To achieve specular light on lightmap static assets, use the Light Modes [Shadowmask](LightMode-Mixed-Shadowmask) or [Distance Shadowmask](LightMode-Mixed-DistanceShadowmask) on Baked lights. This ensures the light is real-time and high quality. See documentation on [Light Modes](LightModes) for more information.)

---

* <span class="page-edit"> 2017-06-08  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Direct Specular removed in 5.6</span>

* <span class="page-history">Light Modes added in 5.6</span>