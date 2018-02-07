# Tree - Wind Zones


__Wind Zones__ add realism to the trees you create by making them wave their branches and leaves as if blown by the wind.


![To the left a Spherical Wind Zone, to the right a Directional Wind zone.](../uploads/Main/InspectorWindZones.png) 

## Properties


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Mode__ ||
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Spherical__ |Wind zone only has an effect inside the radius, and has a falloff from the center towards the edge.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Directional__ |Wind zone affects the entire scene in one direction.|
|__Radius__ |Radius of the Spherical Wind Zone (only active if the mode is set to Spherical).|
|__Main__ |The primary wind force. Produces a softly changing wind pressure.|
|__Turbulence__ |The turbulence wind force. Produces a rapidly changing wind pressure.|
|__Pulse Magnitude__ |Defines how much the wind changes over time.|
|__Pulse Frequency__ |Defines the frequency of the wind changes.|

## Details

__Wind Zones__ are used only by the tree creator for animating leaves and branches. This can help your scenes appear more natural and allows forces (such as explosions) within the game to look like they are interacting with the trees.
For more information about how a tree works, just visit the [tree class page](class-Tree).

##Using Wind Zones in Unity

Using __Wind Zones__ in Unity is really simple. 
First of all, to create a new __wind zone__ just click on __Game Object &gt; 3D Object &gt; Wind Zone__. 

Place the wind zone (depending on the type) near the trees created with the [tree creator](class-Tree) and watch it interact with your trees!.

**Note:** If the wind zone is Spherical you should place it so that the trees you want to blow are within the sphere's radius. If the wind zone is directional it doesn't matter where in the scene you place it. 

##Hints



* To produce a softly changing general wind:
    * Create a directional wind zone.
    * Set Wind Main to 1.0 or less, depending on how powerful the wind should be.
    * Set Turbulence to 0.1.
    * Set Pulse Magnitude to 1.0 or more.
    * Set Pulse Frequency to 0.25.


* To create the effect of a helicopter passing by:
    * Create a spherical wind zone.
    * Set Radius to something that fits the size of your helicopter
    * Set Wind Main to 3.0
    * Set Turbulence to 5.0
    * Set Pulse Magnitude to 0.1
    * Set Pulse Frequency to 1.0
    * Attach the wind zone to a GameObject resembling your helicopter.


* To create the effect of an explosion:
    * Do the same as with the helicopter, but fade the Wind Main and Turbulence quickly to make the effect wear off.

---

* <span class="page-edit">2017-09-19  <!-- include IncludeTextAmendPageSomeEdit --></span>

* <span class="page-history">GameObject menu changed in Unity 4.6</span>