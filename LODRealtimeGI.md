# LOD and Realtime GI

Read this page before you use Realtime Global Illumination (GI) on models which use the [LOD (level of detail)](LevelOfDetail) feature.

When you use Unity’s LOD system in a Scene with baked lighting and Realtime GI, the system lights the most detailed model out of the LOD Group as if it is a regular static model. It uses lightmaps for direct and indirect lighting, and separate lightmaps for Realtime GI.

To allow the baking system to produce real-time or baked lightmaps, select the GameObject you want to affect, view its Renderer component in the Inspector window, and check that __Lightmap Static__ is enabled.

For lower LODs in an LOD Group, you can only combine baked lightmaps with Realtime GI from [Light Probes](LightProbes) or [Light Probe Proxy Volumes](class-LightProbeProxyVolume), which you must place around the LOD Group.

Whenever you use Realtime GI, the Renderer enables the __Light Probes__ option for the lower LODs, even if you enable __Lightmap Static__.

![An animation showing how real-time ambient color affects the Realtime GI used by lower LODs](../uploads/Main/LODRealtimeGI.gif)

---

* <span class="page-edit">2017-10-25  <!-- include IncludeTextAmendPageYesEdit --></span>

* <span class="page-history">Added Realtime Global Illumination in  [2017.3](https://docs.unity3d.com/2017.3/Documentation/Manual/30_search.html?q=newin20173) <span class="search-words">NewIn20173</span></span>