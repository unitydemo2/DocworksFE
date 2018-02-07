# Inherit Velocity module

This module controls how the speed of particles reacts to movement of their parent object over time.

![](../uploads/Main/PartSysInheritVelocity55.png)

## Properties

| **Property**| **Function** |
|:---|:---| 
| __Mode__| Specifies how the emitter velocity is applied to particles |
| &nbsp;&nbsp;&nbsp;&nbsp;Current| The emitter’s current velocity will be applied to all particles on every frame. For example, if the emitter slows down, all particles will also slow down. |
| &nbsp;&nbsp;&nbsp;&nbsp;Initial| The emitter’s velocity will be applied once, when each particle is born. Any changes to the emitter’s velocity made after a particle is born will not affect that particle. |
| __Multiplier__| The proportion of the emitter’s velocity that the particle should inherit. |


## Details

This effect is very useful for emitting particles from a moving object, such as dust clouds from a car, smoke from a rocket, steam from a steam train’s chimney, or any situation where the particles should initially be moving at a percentage of the speed of the object they appear to come from. This module only has an effect on the particles when __Simulation Space__ is set to __World__ in the [Main module](PartSysMainModule).

It is also possible to use curves to influence the effect over time. For example, you could apply a strong attraction to newly created particles, which reduces over time. This could be useful for steam train smoke, which would drift off slowly over time and stop following the train it was emitted from. 