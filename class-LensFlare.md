Lens Flare
==========


__Lens Flares__ simulate the effect of lights refracting inside camera lens. They are used to represent really bright lights or, more subtly, just to add a bit more atmosphere to your scene.


![](../uploads/Main/Inspector-LensFlare.png) 

The easiest way to setup a Lens Flare is just to assign the Flare property of the [Light](class-Light). Unity contains a couple of pre-configured Flares in the [Standard Assets package](HOWTO-InstallStandardAssets).

Otherwise, create an empty __GameObject__ with __GameObject-&gt;Create Empty__ from the menu bar and add the Lens Flare __Component__ to it with __Component-&gt;Effects-&gt;Lens Flare__. Then choose the __Flare__ in the Inspector.

To see the effect of Lens Flare in the __Scene View__, check the __Effect__ drop-down in the Scene View toolbar and choose the Flares option.


![Enable the Fx button to view Lens Flares in the Scene View](../uploads/Main/LensFlare-FXButton.png) 


Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Flare__ |The [Flare](class-Flare) to render. The flare defines all aspects of the lens flare's appearance. |
|__Color__ |Some flares can be colorized to better fit in with your scene's mood. |
|__Brightness__ |How large and bright the Lens Flare is. |
|__Fade Speed__ |How quickly or slowly the flare will fade. |
|__Ignore Layers__ |Select masks for layers that shouldn't hide the flare. |
|__Directional__ |If set, the flare will be oriented along positive Z axis of the game object. It will appear as if it was infinitely far away, and won't track object's position, only the direction of Z axis. |


Details
-------


You can directly set flares as a property of a [Light](class-Light) Component, or set them up separately as Lens Flare component. If you attach them to a light, they will automatically track the position and direction of the light. To get more precise control, use this Component.

A [Camera](class-Camera) has to have a [Flare Layer](class-FlareLayer) Component attached to make Flares visible (this is true by default, so you don't have to do any set-up).


Hints
-----



* Be discrete about your usage of Lens Flares.
* If you use a very bright Lens Flare, make sure its direction fits with your scene's primary light source.
* To design your own Flares, you need to create some Flare Assets. Start by duplicating some of the ones we provided in the the __Lens Flares__ folder of the Standard Assets, then modify from that.
* Lens Flares are blocked by __Colliders__. A Collider in-between the Flare GameObject and the Camera will hide the Flare, even if the Collider does not have a __Mesh Renderer__. If the in-between Collider is marked as Trigger it will block the flare if and only if __Physics.queriesHitTriggers__ is true.
