#Advanced Reflection Probe Features

Two further features which can improve the visual realism obtained from [Reflection Probes](ReflectionProbes) are described below: **Interreflections** and **Box Projection**.


##Interreflections

You may have seen a situation where two mirrors are placed fairly close together and facing each other. Both mirrors reflect not only the mirror opposite but also the reflections produced by that mirror. The result is an endless progression of reflections between the two; reflection between objects like this are known as **Interreflections**.

Reflection probes create the cubemap by taking a snapshot of the view from their position. However, with a single snapshot, the view cannot show interreflections and so additional snapshots must be taken for each stage in the interreflection sequence.

The number of times that a reflection can "bounce" back and forth between two objects is controlled in the [Lighting window](GlobalIllumination); go to __Environment__ > __Environment Reflections__ and edit the __Bounces__ property. This is set globally for all probes, rather than individually for each probe. With a reflection bounce count of 1, reflective objects viewed by a probe are shown as black. With a count of 2, the first level of interreflection are visible, with a count of 3, the first two levels will be visible, and so on. 

Note that the reflection bounce count also equals the number of times the probe must be baked with a corresponding increase in the time required to complete the full bake. You should therefore set the count higher than one only when you know that reflective objects will be clearly visible in one or more probes.


##Box projection

Normally, the reflection cubemap is assumed to be at an infinite distance from any given object. Different angles of the cubemap will be visible as the object turns but it is not possible for the object to move closer or farther away from the reflected surroundings. This often works very well for outdoor scenes but its limitations show in an indoor scene; the interior walls of a room are clearly not an infinite distance away and the reflection of a wall should get larger the closer the object gets to it.

The __Box Projection__ option allows you to create a reflection cubemap at a finite distance from the probe, thus allowing objects to show different-sized reflections according to their distance from the cubemap's walls. The size of the surrounding cubemap is determined by the probes zone of effect, as determined by its __Box Size__ property. For example, with a probe that reflects the interior of a room, you should set the size to match the dimensions of the room. Globally, you can enable __Box Projection__ from __Project Settings__ > __Graphics__ > __Tier Settings__, but the option can be turned off from the Reflection Probe inspector for specific Reflection Probes when infinite projection is desired.


![The parallax issue is fixed by using Box Projection option](../uploads/Main/GraphicsSettings_BoxProjection.png)

