# Light Probes

__Light Probes__ provide a way to capture and use information about light that is passing through the empty space in your scene.

Similar to lightmaps, light probes store "baked" information about lighting in your scene. The difference is that while lightmaps store lighting information about light hitting the *surfaces* in your scene, light probes store information about light passing through *empty space* in your scene.

![An extremely simple scene showing light probes placed around two cubes](../uploads/Main/LightProbes-0.png)

Light Probes have two main uses:

The primary use of light probes is to provide high quality lighting (including indirect bounced light) on moving objects in your scene.

The secondary use of light probes is to provide the lighting information for static scenery when that scenery is using Unity’s __LOD system__. 

When using light probes for either of these two distinct purposes, many of the techniques you need to use are the same. It’s important to understand how light probes work so that you can choose where to place your probes in the scene.

---

* <span class="page-edit"> 2017-06-08  <!-- include IncludeTextNewPageNoEdit --></span>

* <span class="page-history">Light Probes updated in 5.6</span>