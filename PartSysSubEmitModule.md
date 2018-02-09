#Sub Emitters module

This module allows you to set up sub-emitters. These are additional particle emitters that are created at a particle's position at certain stages of its lifetime.

![](../uploads/Main/PartSysSubEmitInsp.png)

##Properties

|**_Property_** |**_Function_** |
|:---|:---|
|__Sub Emitters__|Configure a list of sub-emitters and select their trigger condition as well as what properties they inherit from their parent particles. |


##Details

Many types of particles produce effects at different stages of their lifetimes that can also be implemented using Particle Systems. For example, a bullet might be accompanied by a puff of powder smoke as it leaves the gun barrel, and a fireball might explode on impact. You can use sub-emitters to create effects like these. 

Sub-emitters are ordinary Particle System objects created in the Scene or from Prefabs. This means that sub-emitters can have sub-emitters of their own (this type of arrangement can be useful for complex effects like fireworks). However, it is very easy to generate an enormous number of particles using sub-emitters, which can be resource-intensive.

There are three conditions that you can use to trigger a sub-emitter:

* __Birth__: When the particle is created
* __Collision__: When the particle collide with an object
* __Death__:  When the particle are destroyed

Note that the __Collision__ and __Death__ events can only use burst emission in the [Emission](PartSysEmissionModule) module.

Additionally, you can transfer properties from the parent particle to each newly created particle using the __Inherit__ options. It’s possible to transfer any combination of size, rotation, and color. To control how velocity is inherited, configure the [Inherit Velocity](PartSysInheritVelocity) module on the sub-emitter system.