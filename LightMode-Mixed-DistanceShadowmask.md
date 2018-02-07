# Distance Shadowmask

__Distance Shadowmask__ is a version of the __Shadowmask__ lighting mode. It is shared by all Mixed Lights in a Scene. To set __Mixed lighting__ to __Distance Shadowmask__: 

* Open the Lighting window (menu: __Window__ > __Lighting__ > __Settings__), click the __Scene__ tab, navigate to __Mixed Lighting__, and set the __Lighting Mode__ to __Shadowmask__. 
* Next, open the __Quality Settings__ (menu: __Edit__ > __Project Settings__ > __Quality__), navigate to __Shadowmask Mode__ and set it to __Distance Shadowmask__. 

See documentation on [Mixed lighting](LightMode-Mixed) to learn more about this lighting mode, and see documentation on [Light modes](LightModes) to learn more about the other modes available. 

A shadow mask is a Texture that shares the same UV layout and resolution with its corresponding light map. It stores occlusion information for up to 4 lights per texel, because Textures are limited to up to 4 channels on current GPUs.

The __Distance Shadowmask__ mode is a version of the __Shadowmask__ lighting mode that includes high quality shadows cast from static GameObjects onto dynamic GameObjects.

Within the __Shadow Distance__ (menu: __Edit__ > __Project Settings__ > __Quality__ > __Shadows__), Unity renders both dynamic and static GameObjects into the shadow map, allowing static GameObjects to cast sharp shadows onto dynamic GameObjects. For this reason, __Distance Shadowmask__ mode has higher performance requirements than __Shadowmask__ mode, because all static GameObjects in the scene are rendered into the shadow map.


Beyond the __Shadow Distance__:

* Static GameObjects receive high-resolution shadows from other static GameObjects via the precomputed shadow mask.
* Dynamic GameObjects receive low-resolution shadows from static GameObjects via [Light Probes](LightProbes).

A good example of when __Distance Shadowmask__ mode might be useful is if you are building an open world Scene with shadows up to the horizon, and complex static Meshes casting real-time shadows on moving characters.

## Shadows

The following table shows how static and dynamic GameObjects cast and receive shadows when using __Distance Shadowmask__ mode:

| | __Dynamic receiver__<br/>A dynamic GameObject that is receiving a shadow from another static or dynamic GameObject |  | __Static receiver__<br/>A static GameObject that is receiving a shadow from another static or dynamic GameObject||
|:---|:---|:---|:---|:---| 
| | Within Shadow Distance | Beyond Shadow Distance | Within Shadow Distance | Beyond Shadow Distance |
| __Dynamic caster__<br/>A dynamic GameObject that is casting a shadow| Shadow map | - | Shadow map | - |
| __Static caster__<br/>A static GameObject that is casting a shadow| Shadow map | Light Probes | Shadow map | Shadow mask |



## Advantages and disadvantages of Distance Shadowmask mode

The performance requirements of __Distance Shadowmask__ mode make it a good option for building to high-end PCs and current generation consoles. These are the most significant advantages and disadvantages of using __Distance Shadowmask__ mode:

### Advantages

* It provides the same visual effect as [Realtime Lighting](LightMode-Realtime).
* It provides real-time shadows from dynamic GameObjects onto static GameObjects, and static GameObjects onto dynamic GameObjects.
* One Texture operation in the Shader handles all lighting and shadows between static GameObjects.
* It automatically composites dynamic and static shadows.
* It provides indirect lighting.

### Disadvantages

* It only allows up to 4 overlapping light volumes (see documentation under the 'Technical details' section of [Mixed lighting](LightMode-Mixed) for more information).
* It has increased memory requirements for light map Texture sets.
* It has increased memory requirements for shadow mask Textures.
* It has increased performance requirements, because Unity renders light and shadow from static GameObjects into shadow maps.

---

* <span class="page-edit"> 2017-09-18 <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Light Modes added in 5.6</span>