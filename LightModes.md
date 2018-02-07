# Lighting Modes

This page assumes you have already read documentation on [lighting in Unity](LightingInUnity).

To control lighting precomputation and composition in Unity, you need to assign a __Light Mode__ to a Light. This __Light Mode__ defines the Light’s intended use. To assign a Light Mode, select the Light in your Scene and, in the [Light Inspector window](GlobalIllumination), select __Mode__.  

![](../uploads/Main/LightModes-0.png)

The Modes and their possible mappings are:

* [Realtime](LightMode-Realtime)
* [Mixed](LightMode-Mixed) - Mixed Lights have their own sub-modes. Set these in the Lighting window:
    * [Baked Indirect](LightMode-Mixed-BakedIndirect)
    * [Shadowmask](LightMode-Mixed-DistanceShadowmask)
    * [Distance Shadowmask](LightMode-Mixed-Shadowmask)
    * [Subtractive](LightMode-Mixed-Subtractive)
* Baked(LightMode-Baked)

For more information, see the [Reference card for Light Modes](https://drive.google.com/open?id=1v-LnDOJcsSsa0ViF7kBs6xgY9Q_z-1k6h95LE0lf46U).

The Modes are listed above in the order of least to most light path precomputations required (See *How Modes work*, below). Note that this order does not necessarily correlate with the amount of time the actual precomputation requires.

## How Modes work

Each __Mode__ in the Light Inspector window corresponds to a group of settings in the Lighting window (menu: __Window__ > __Lighting__ > __Settings__ > __Scene__). 

![The available __Light Modes__ in the Light component (left), and the corresponding settings available for those modes in the Lighting Scene window (right).](../uploads/Main/LightModes-1.png)

| __Light Inspector__| __Lighting window__ | __Function__ |
|:---|:---|:---| 
| __Realtime__| __Realtime Lighting__ | Unity calculates and updates the lighting of __Realtime__ Lights every frame during run time. No Realtime Lights are precomputed. |
| __Mixed__| __Mixed Lighting__ | Unity can calculate some properties of __Mixed__ Lights during run time, but only within strong limitations. Some Mixed Lights are precomputed. |
| __Baked__| __Lightmapping Settings__ | Unity pre-calculates the illumination from __Baked__ Lights before run time, and does not include them in any run-time lighting calculations. All Baked Lights are precomputed. |

Use these settings to adjust each mode. The adjustments you make apply to all Lights with that Mode assigned to them. For example, if you open the Lighting window, navigate to the __Realtime Lighting Settings__ and tick __Realtime Global Illumination__, all Lights that have their __Mode__ set to __Realtime__ mode use __Realtime Global Illumination__.

Precomputation yields two sets of results:

* Unity stores results for static GameObjects as Texture atlases in UV Texture coordinate space. Unity provides several settings to [control this layouting](GlobalIllumination). 

* [Light Probes](LightProbes) store a representation of light in empty space as seen from their particular position. Dynamic GameObjects moving through this portion of empty space use this information to receive illumination from the precomputed lighting.

---

* <span class="page-edit"> 2017-06-08  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Updated in 5.6</span>