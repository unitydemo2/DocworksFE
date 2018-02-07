# LOD for baked lightmaps

This page provides advice on baking light into models that use Unity's [LOD (level of detail)](LevelOfDetail) system. 

When you use Unity’s LOD system in a Scene with baked lighting, the system lights the most detailed model out of the LOD Group as if it is a regular static model. It uses lightmaps for the direct and indirect lighting, and separate lightmaps for Realtime GI.

When you use the Enlighten lightmapper, the system only bakes the direct lighting, and the LOD system relies on [Light Probes](LightProbes) to sample indirect lighting. 

To make sure your lower LOD models look correct with baked light, you must position Light Probes around them to capture the indirect lighting during the bake. Otherwise, your lower LOD models look incorrect, because they only receive direct light:

![The LOD 1 and LOD 2 models here are lit incorrectly because light probes have not been placed around the model in the scene. They only show direct lighting.](../uploads/Main/LODForBakedGI-1.png)

To set up LOD models correctly for baked lighting, mark the LOD GameObjects as __Lightmap Static__. To do this, select the GameObject, and at the top of the Inspector window, select the drop-down menu next to the __Static__ checkbox:

![In this example, the LODs are assumed to be children of this GameObject](../uploads/Main/LODForBakedGI-2.png)

Use the [Light Probes component](LightProbes) to place Light Probes around the LOD GameObjects.

![Light probes placed around an LOD model.](../uploads/Main/LODForBakedGI-3.png)

**Note**: Only the most detailed model affects the lighting on the surrounding geometry (for example, shadows or bounced light on surrounding buildings). In most cases this should not be a problem, because your lower level-of-detail models should closely resemble the highest level-of-detail model.

When you use the __Progressive Lightmapper__, there is no need to place Light Probes around the LOD Group to generate baked indirect lighting. However, to make Realtime GI affect the Renderers in the LOD Group, you must include the Light Probes.

---

* <span class="page-edit">2017-10-20  <!-- include IncludeTextAmendPageYesEdit --></span>

* <span class="page-history">Updated in 5.6</span>

* <span class="page-history">Updated in 2017.3</span>