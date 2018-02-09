# Lightmapping modes

|**5.6 DRAFT ADDITION TO DOCUMENTATION** |
|:---|
|This feature has additional or changed functionality in Unity 5.6. The link below is first draft document of that addition or change. As such, the information in this document may be subject to change before final release.<br/><br/>See first draft [Light Modes](https://docs.google.com/document/d/116JvLXljfbdfllOLlyzVvWmNWpbUwcYKV16blVHuS2E/edit) documentation.|
|**NOTE:** **Directional lightmaps** are now called **Lightmapping modes**.|

**Directional lightmaps** store more information about the lighting environment than regular lightmaps. Shaders can use that extra data about incoming light to better calculate outgoing light, which is how materials appear on the screen. This happens at the cost of increased texture memory usage and shading time.

You can choose one of three modes: **Non-directional**, **Directional** and **Directional with Specular**. All three are available as **realtime** and **baked** lightmaps.

* **Non-directional: flat diffuse.** This mode uses just a single lightmap, storing information about how much light does the surface emit, assuming it's purely diffuse. Objects lit this way will appear flat (normalmaps won't be used) and diffuse (even if the material is specular), but otherwise will be lit correctly. These barrels are using baked lightmaps. The only detail definition comes from a reflection probe and an occlusion map.

![](../uploads/Main/DirectionalLightmapping1.png) 

* **Directional: normalmapped diffuse.** This mode adds a secondary lightmap, which stores the incoming dominant light direction and a factor proportional to how much light in the first lightmap is the result of light coming in along the dominant direction. The rest is then assumed to come uniformly from the entire hemisphere. That information allows the material to be normalmapped, but it will still appear purely diffuse.

![](../uploads/Main/DirectionalLightmapping2.png) 


* **Directional with Specular: full shading.** Like the previous mode, this one uses two lightmaps: light and direction, but this time they're split in halves. Left side stores direct light, and right indirect. Unlike the two other modes, light is stored as incoming intensity. That extra information allows the shader to run the same BRDF that's usually reserved for realtime lights, resulting in a full-featured material appearance - now also interacting with indirect light.

![](../uploads/Main/DirectionalLightmapping3.png) 

**Performance:** the Directional mode uses twice as much texture memory as Non-directional lightmaps and has a slightly higher shading cost. Directional with Specular uses twice as much texture memory as Directional (it also uses two textures per set, but they're split in two, so twice as many sets are needed). Its shading cost is comparable to two un-shadowed lights, as it runs the BRDF twice - for direct and indirect light.
Non-directional: one texture, one texture sample, a few extra shader instructions.
Directional: two textures, two texture samples, a few more extra shader instructions.
Directional with Specular: two textures, four texture samples, high extra shader cost (about two un-shadowed lights).

Realtime lightmaps take advantage of the same approach, and are subject to the same shading quality/cost tradeoffs. The only difference from the list above is that the Realtime Directional with Specular lightmap uses three textures (incoming intensity, direction, normal), taking three texture samples. It has a shading cost of one un-shadowed light, as it runs the BRDF only once. It works in combination with a realtime direct light, of course, which has its own shading cost.

The BRDF that is actually used for indirect light (Directional with Specular realtime and the indirect part of baked) is a slightly less expensive version. ``UNITY_BRDF_PBS_LIGHTMAP_INDIRECT`` is defined in ``UnityPBSLighting.cginc``.

The Directional with Specular mode pushes the lightmapper to the limits of the GI technique it uses, which in some cases leads to artifacts. These are most often patches of incorrect dominant light direction, causing dark or black shading. Some of these issues can be fixed increasing the Realtime/Indirect Resolution. If all else fails, the simpler lightmap modes are more robust.