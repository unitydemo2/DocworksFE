# Baked Indirect mode

__Baked Indirect__ mode is a lighting mode shared by all __Mixed Lights__ in a Scene. To set Mixed lighting to __Baked Indirect__, open the Lighting window (menu: __Window__ > __Lighting__ > __Settings__), click the __Scene__ tab, navigate to __Mixed Lighting__ and set the __Lighting Mode__ to __Baked Indirect__. See documentation on [Mixed lighting](LightMode-Mixed) to learn more about this lighting mode, and see documentation on [Light modes](LightModes) to learn more about the other modes available.  

For Lights that are set to __Baked Indirect__ mode, Unity only precomputes indirect lighting, and does not carry out shadow pre-computations. Shadows are fully real-time within the __Shadow Distance__ (menu: __Edit__ > __Project Settings__ > __Quality__ > __Shadows__). In other words, __Baked Indirect__ Lights behave like [Realtime Lights](LightMode-Realtime) with additional indirect lighting, but with no shadows beyond the __Shadow Distance__. You can use effects like the [Post-processing fog effect](PostProcessing-Fog) to obscure the missing shadows past that distance.

A good example of when __Baked Indirect__ mode might be useful is if you are building an indoor shooter or adventure game set in rooms connected with corridors. The viewing distance is limited, so everything that is visible should usually fit within the __Shadow Distance__. This mode is also useful for building a foggy outdoor Scene, because you can use the fog to hide the missing shadows in the distance.

## Shadows

The following table shows how static and dynamic GameObjects cast and receive shadows when using __Baked Indirect__ mode:

| | __Dynamic receiver<br/>__A dynamic GameObject that is receiving a shadow from another static or dynamic GameObject |  | __Static receiver<br/>__A static GameObject that is receiving a shadow from another static or dynamic GameObject ||
|:---|:---|:---|:---|:---| 
| | Within Shadow Distance | Beyond Shadow Distance | Within Shadow Distance | Beyond Shadow Distance |
| __Dynamic caster<br/>__A dynamic GameObject that is casting a shadow| Shadow map | - | Shadow map | - |
| __Static caster<br/>__A static GameObject that is casting a shadow| Shadow map | - | Shadow map | - |

## Advantages and disadvantages of Baked Indirect mode

The performance requirements of __Baked Indirect__ mode make it a good option for building to mid-range PCs and high-end mobile devices. These are the most significant advantages and disadvantages of using __Baked Indirect__ mode:

### Advantages

* It provides the same visual effect as [Realtime Lighting](LightMode-Realtime).
* It provides real-time shadows for all combinations of static and dynamic GameObjects.
* It provides indirect lighting.

### Disadvantages

* It has higher performance requirements relative to other __Mixed__ Light modes, because it renders shadow-casting static GameObjects into shadow maps.
* Shadows do not render beyond the __Shadow Distance__.

---

* <span class="page-edit"> 2017-06-08  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Light Modes added in 5.6</span>