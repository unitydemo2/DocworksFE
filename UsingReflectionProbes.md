#Using Reflection Probes

You can add the [Reflection Probe](class-ReflectionProbe) component to any object in a Scene but it's standard to add each probe to a separate empty GameObject. The usual workflow is:

* Create a new empty GameObject (menu: __GameObject__ > __Create Empty__) and then add the Reflection Probe component to it (menu: __Component__ > __Rendering__ > __Reflection Probe__). Alternatively, if you already have a probe in the scene you will probably find it easier to duplicate that instead (menu: __Edit__ > __Duplicate__).
* Place the new probe in the desired location and set its __Offset__ point and the size of its zone of effect.
* Optionally set other properties on the probe to customise its behaviour.
* Continue adding probes until all required locations have been assigned.

To see the reflections, you will also need at least one reflective object in the scene. A simple test object can be created as follows:

* Add a primitive object such as a Sphere to the scene (menu: __GameObject__ > __3D Object__ > __Sphere__).
* Create a new material (menu: __Assets__ > __Create__ > __Material__) and leave the default __Standard__ shader in place.
* Make the material reflective by setting both the __Metallic__ and __Smoothness__ properties to __1.0__.
* Drag the newly-created material onto the sphere object to assign it.

The sphere can now show the reflections obtained from the probes. A simple arrangement with a single probe is enough to see the basic effect of the reflections.

Finally, the probes must be baked before the reflections become visible. If you have the __Auto Generate__ option enabled in the [Lighting window](GlobalIllumination) (this is the default setting) then the reflections will update as you position or change objects in the scene, although the response is not instantaneous. If you disable auto baking then you must click the __Bake__ button in the Reflection Probe inspector to update the probes. The main reason for disabling auto baking is that the baking process can take quite some time for a complicated scene with many probes.

##Positioning probes

The position of a probe is primarily determined by the position of its GameObject and so you can simply drag the object to the desired location. Having done this, you should set the probe’s zone of effect; this is an axis-aligned box shape whose dimensions are set by the __Box Size__ property. You can set the size values directly or enable the size editing mode in the inspector and drag the sides of the box in the Scene view (see the [Reflection Probe](class-ReflectionProbe) component page for details). The zones of the full set of probes should collectively cover all areas of the scene where a reflective object might pass.

You should place probes close to any large objects in the scene that would be reflected noticeably. Areas around the centres and corners of walls are good candidate locations for probes. Smaller objects might require probes close by if they have a strong visual effect. For example, you would probably want the flames of a campfire to be reflected even if the object itself is small and otherwise insignificant.

When you have probes in all the appropriate places, you then need to define the zone of effect for each probe, which you can do using the __Box Size__ property as mentioned above. A wall might need just a single probe zone along most of its length (at least if it has a fairly uniform appearance) but the zone might be relatively narrow in the direction perpendicular to the wall; this would imply that the wall is only reflected by objects that are fairly close to it. An open space whose appearance varies little from place to place can often be covered by a single probe. Note that a probe’s zone is aligned to the main world axes (X, Y and Z) and can’t be rotated. This means that sometimes a group of probes might be needed along a uniform wall if it is not axis-aligned.


By default, a probe’s zone of effect is centred on its view point but this may not be the ideal position for capturing the reflection cubemap. For example, the probe zone for a very high wall might extend some distance from the wall but you might want the reflection to be captured from a point close to it rather than the zone’s centre. You can optionally add an offset to view point using the __Box Offset__ property (ie, the offset is the position in the GameObject’s local space that the probe’s cubemap view is generated from). Using this, you can easily place the view point anywhere within the zone of effect or indeed outside the zone altogether.


##Overlapping probe zones

It would be very difficult to position the zones of neighbouring reflection probes without them overlapping and fortunately, it is not necessary to do so. However, this leaves the issue of choosing which probe to use in the overlap areas. By default, Unity calculates the intersection between the reflective object’s bounding box and each of the overlapping probe zones; the zone which has the largest volume of intersection with the bounding box is the one that will be selected.

![Probe A is selected since its intersection with the object is larger](../uploads/Main/ProbeZoneOverlap.svg)

You can modify the calculation using the probes’ __Importance__ properties. Probes with a higher importance value have priority over those of lower importance within overlap zones. This is useful, say, if you have a small probe zone that is contained completely inside a larger zone (ie, the intersection of the character’s bounding box with the enclosing zone might always be larger and so the small zone would never be used).


###Blending

To enable Reflection Probe blending, navigate to __Graphic Settings__ > __Tier settings__. With blending enabled, Unity will gradually fade out one probe’s cubemap while fading in the other’s as the reflective object passes from one zone to the other. This gradual transition avoids the situation where a distinctive object suddenly “pops” into the reflection as an object crosses the zone boundary.

Blending is controlled using the __Reflection Probes__ property of the [Mesh Renderer](class-MeshRenderer) component. Four blending options are available:

* __Off__ - Reflection probe blending is disabled. Only the skybox will be used for reflection
* __Blend Probes__ - Blends only adjacent probes and ignores the skybox. You should use this for objects that are “indoors” or in covered parts of the scene (eg, caves and tunnels) since the sky is not visible from these place and so should never appear in the reflections.
* __Blend Probes and Skybox__ - Works like _Blend Probes_ but also allows the skybox to be used in the blending. You should use this option for objects in the open air, where the sky would always be visible.
* __Simple__ - Disables blending between probes when there are two overlapping reflection probe volumes.

When probes have equal __Importance__ values, the blending weight for a given probe zone is calculated by dividing its intersection (volume) with the object’s bounding box by the sum of all probes’ intersections with the box. For example, if the box intersects probe A’s zone by 1.0 cubic units and intersects probe B’s zone by 2.0 cubic units then the blending values will be:

* Probe A: 1.0 / (1.0 + 2.0) = 0.33
* Probe B: 2.0 / (1.0 + 2.0) = 0.67

In other words, the blend will incorporate 33% of probe A's reflection and 67% of probe B's reflection.

The calculation must be handled slightly differently in the case where one probe is entirely contained within the other, since the inner zone overlaps entirely with the outer. If the object’s bounding box is entirely within the inner zone then that zone’s blending weight is 1.0 (ie, the outer zone is not used at all). When the object is partially outside the inner zone, the intersection volume of its bounding box with the inner zone is divided by the total volume of the box. For example, if the intersection volume is 1.0 cubic units and the bounding box’s volume is 4.0 cubic units, then the blending weight of the inner probe will be 1.0 / 4.0 = 0.25. This value is then subtracted from 1.0 to get the weight for the outer probe which in this case will be 0.75.

When one probe involved in the blend has a higher __Importance__ value than another, the more important probe overrides the other in the usual way.
<br/>
<br/>

---

* <span class="page-history">Updated in 5.6</span>

* <span class="page-edit">2017-06-06  <!-- include IncludeTextNewPageSomeEdit --></span>

