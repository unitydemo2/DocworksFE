# Subtractive mode

__Subtractive__ mode is a lighting mode shared by all Mixed Lights in a Scene. To set Mixed lighting to __Subtractive__, open the Lighting window (menu: __Window__ > __Lighting__ > __Settings__), click the __Scene__ tab, navigate to __Mixed Lighting__ and set the __Lighting Mode__ to __Subtractive__. See documentation on [Mixed lighting](LightMode-Mixed) to learn more about this lighting mode, and see documentation on [Light modes](LightModes) to learn more about the other modes available. 

__Subtractive__ is the only Mixed lighting mode that bakes direct lighting into the light map, and discards the information that Unity uses to composite dynamic and static shadows in other Mixed lighting modes. Because the Light is already baked into the lightmap, Unity cannot perform any direct lighting calculations at run time. 

In __Subtractive__ mode:

* Static GameObjects do not show any specular or glossy highlights at all from Mixed Lights. They also cannot receive any shadows from dynamic GameObjects, except for the main Directional Light (see paragraph below for more information on this). 

* Dynamic GameObjects receive real-time lighting, and support glossy reflections. However, they can only receive shadows from static GameObjects via [Light Probes](LightProbes).

In __Subtractive__ mode, the main Directional Light (which is usually the sun) is the only light source which casts real-time shadows from dynamic GameObjects onto static GameObjects. Shadows cast from static GameObjects onto other static GameObjects are baked into the lightmap, even for the main Light, so Unity cannot guarantee correct composition of baked and real-time shadows. __Subtractive__ mode therefore has a [Realtime Shadow Color](https://docs.google.com/document/d/1SEkozSX298iM6N1MONyss8IA2B5rtrfTStE72Tul2Y0/edit) field. Unity uses this color in the Shader to composite real-time shadows with baked shadows. To do this, it reduces the effect of the light map in areas shadowed by dynamic GameObjects. Because there is no correct value that the engine can predetermine, choosing a value that works for any given Scene is down to your own artistic choice.

A good example of when __Subtractive__ mode might be useful is when you are building a cel-shaded (that is, cartoon-style) game with outside levels and very few dynamic GameObjects.

## Shadows

The following table shows how static and dynamic GameObjects cast and receive shadows when using __Subtractive__ mode:

| | __Dynamic receiver<br/>__A dynamic GameObject that is receiving a shadow from another static or dynamic GameObject |  | __Static receiver<br/>__A static GameObject that is receiving a shadow from another static or dynamic GameObject||
|:---|:---|:---|:---|:---| 
| | Within Shadow Distance | Beyond Shadow Distance | Within Shadow Distance | Beyond Shadow Distance |
| __Dynamic caster<br/>__A dynamic GameObject that is casting a shadow| Shadow map | - | Main light shadow map | -|
| __Static caster<br/>__A static GameObject that is casting a shadow| Light Probes | Light Probes | Lightmap | Lightmap |



## Advantages and disadvantages of Subtractive mode

The performance requirements of __Subtractive__ mode make it a good option for building to low-end mobile devices. These are the most significant advantages and disadvantages of using __Subtractive__ mode:

### Advantages

* It provides high-quality shadows between static GameObjects in lightmaps at no additional performance requirement.

* One Texture operation in the Shader handles all lighting and shadows between static GameObjects.

* It provides indirect lighting.

### Disadvantages

* It does not provide real-time direct lighting, and therefore does not provide specular lighting.

* It does not provide dynamic shadows on static GameObjects, except for one Directional Light (the main Light).

* It only provides low-resolution shadows from static GameObjects onto dynamic GameObjects, via Light Probes.

* It provides inaccurate composition of dynamic and static shadows.

* It has increased memory requirements for the light map texture set (compared to no lightmaps).

---

* <span class="page-edit"> 2017-06-08  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Light Modes added in 5.6</span>

