# Shadowmask

__Shadowmask__ is a version of the __Shadowmask__ lighting mode shared by all Mixed Lights in a Scene. To set Mixed lighting to __Shadowmask__:

* Open the Lighting window (menu: __Window__ > __Lighting__ > __Settings__), click the __Scene__ tab, navigate to __Mixed Lighting__ and set the __Lighting Mode__ to __Shadowmask__.
* Next, open the __Quality Settings__ (menu: __Edit__ > __Project Settings__ > __Quality__), navigate to __Shadowmask Mode__ and set it to __Shadowmask__.

See documentation on [Mixed lighting](LightMode-Mixed) to learn more about this lighting mode, and see documentation on [Light modes](LightModes) to learn more about the other modes available.

A shadow mask is a Texture that shares the same UV layout and resolution with its corresponding lightmap. It stores occlusion information for up to 4 lights per texel, because Textures are limited to up to 4 channels on current GPUs.

Unity precomputes shadows cast from static GameObjects onto other static GameObjects, and stores them in a separate Shadowmask Texture for up to 4 overlapping lights. If more than 4 lights overlap, any additional lights fall back to [Baked Lighting](LightMode-Baked). Which of the lights fall back to [Baked Lighting](LightMode-Baked) is determined by the baking system and stays consistent across bakes, unless one of the lights overlapping is modified. [Light Probes](LightProbes) also receive the same information for up to 4 lights.

Light overlapping is computed independently of shadow receiving objects. So, an object can get the influence of 10 different mixed lights all from the same Shadowmask/Probe channel, as long as those light bounding volumes don't overlap at any point in space. If some lights overlap then more channels are used. And, if a light does overlap while all 4 channels have already been assigned, that light will fallback to fully baked.

In __Shadowmask__ mode:

* Static GameObjects receive shadows from other static GameObjects via the shadow mask, regardless of the __Shadow Distance__ (menu: __Edit__ > __Project Settings__ > __Quality__ > __Shadows__). They also receive shadows from dynamic GameObjects, but only those within the __Shadow Distance__.

* Dynamic GameObjects receive shadows from other dynamic GameObjects within the __Shadow Distance__ via shadow maps. They also receive shadows from static GameObjects, via Light Probes. The shadow fidelity depends on the density of Light Probes in the Scene, and the __Light Probes__ mode selected on the Mesh Renderer.

Unity automatically composites overlapping shadows from static and dynamic GameObjects, because shadow masks (which hold static GameObject lighting and shadow information) and shadow maps (which hold dynamic GameObject lighting and shadow information) only encode occlusion information.

A good example of when __Shadowmask__ mode might be useful is if you are building an almost fully static Scene, using specular Materials, soft baked shadows and a dynamic shadow caster, not too close to the camera. Another good example is an open-world Scene with baked shadows up to the horizon, but without dynamic lighting such as a day/night cycle.

## Shadows

The following table shows how static and dynamic GameObjects cast and receive shadows when using __Shadowmask__ mode:

| | __Dynamic receiver__<br/> A dynamic GameObject that is receiving a shadow from another static or dynamic GameObject |  | __Static receiver__<br/> A static GameObject that is receiving a shadow from another static or dynamic GameObject||
|:---|:---|:---|:---|:---| 
| | Within Shadow Distance | Beyond Shadow Distance | Within Shadow Distance | Beyond Shadow Distance |
| __Dynamic caster__<br/> A dynamic GameObject that is casting a shadow| Shadow map | - | Shadow map | - |
| __Static caster__<br/> A static GameObject that is casting a shadow| Light Probes | Light Probes | Shadowmask | Shadowmask |

## Advantages and disadvantages of Shadowmask mode

The performance requirements of __Shadowmask__ mode make it a good option for building to low and mid-range PCs, and mobile devices. These are the most significant advantages and disadvantages of using __Shadowmask__ mode:

### Advantages

* It offers the same visual effect as [Realtime Lighting](LightMode-Realtime).

* It provides real-time shadows from dynamic GameObjects onto static GameObjects.

* One Texture operation in the Shader handles all lighting and shadows between static GameObjects.

* It automatically composites overlapping shadows from static and dynamic GameObjects.

* It has mid-to-low performance requirements, because it does not render static GameObjects into shadow maps.

* It provides indirect lighting.

### Disadvantages

* It only provides low-resolution shadows from static GameObjects onto dynamic GameObjects, via Light Probes.

* It only allows up to 4 overlapping light volumes (see documentation under the ‘Technical details’ section of [Mixed Lighting](LightMode-Mixed) for more information).

* It has increased memory requirements for the light map Texture set.

* It has increased memory requirements for the shadow mask Texture.

---

* <span class="page-edit"> 2017-09-18  <!-- include IncludeTextAmendPageSomeEdit --></span>

* <span class="page-history">Light Modes added in 5.6</span>
* <span class="page-history">Added advice on light overlap computation in Unity 2017.1</span>