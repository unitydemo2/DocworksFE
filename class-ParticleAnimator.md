Particle Animator (Legacy)
==========================


__Particle Animators__ move your particles over time, you use them to apply wind, drag & color cycling to your particle systems.


![](../uploads/Main/Inspector-ParticleAnimator.png) 


Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Does Animate Color__ |If enabled, particles cycle their color over their lifetime. |
|__Color Animation__ |The 5 colors particles go through. All particles cycle over this - if some have a shorter life span than others, they will animate faster. |
|__World Rotation Axis__ |An optional world-space axis the particles rotate around. Use this to make advanced spell effects or give caustic bubbles some life. |
|__Local Rotation Axis__ |An optional local-space axis the particles rotate around. Use this to make advanced spell effects or give caustic bubbles some life. |
|__Size Grow__ |Use this to make particles grow in size over their lifetime. As randomized forces will spread your particles out, it is often nice to make them grow in size so they don't fall apart. Use this to make smoke rise upwards, to simulate wind, etc. |
|__Rnd Force__ |A random force added to particles every frame. Use this to make smoke become more alive. |
|__Force__ |The force being applied every frame to the particles, measure relative to the world. |
|__Damping__ |How much particles are slowed every frame. A value of 1 gives no damping, while less makes them slow down. |
|__Autodestruct__ |If enabled, the GameObject attached to the Particle Animator will be destroyed when all particles disappear. |

Details
-------


Particle Animators allow your particle systems to be dynamic. They allow you to change the color of your particles, apply forces and rotation, and choose to destroy them when they are finished emitting. For more information about Particle Systems, reference [Mesh Particle Emitters](class-MeshParticleEmitter), [Ellipsoid Particle Emitters](class-EllipsoidParticleEmitter), and [Particle Renderers](class-ParticleRenderer).


###Animating Color

If you would like your particles to change colors or fade in/out, enable them to __Animate Color__ and specify the colors for the cycle. Any particle system that animates color will cycle through the 5 colors you choose. The speed at which they cycle will be determined by the Emitter's __Energy__ value.

If you want your particles to fade in rather than instantly appear, set your first or last color to have a low Alpha value.


![An Animating Color Particle System](../uploads/Main/ParticleRainbow.png) 


###Rotation Axes

Setting values in either the Local or World __Rotation Axes__ will cause all spawned particles to rotate around the indicated axis (with the __Transform's__ position as the center). The greater the value is entered on one of these axes, the faster the rotation will be.

Setting values in the Local Axes will cause the rotating particles to adjust their rotation as the Transform's rotation changes, to match its local axes.

Setting values in the World Axes will cause the particles' rotation to be consistent, regardless of the Transform's rotation.


###Forces & Damping

You use force to make particles accelerate in the direction specified by the force.

__Damping__ can be used to decelerate or accelerate without changing their direction:

* A value of 1 means no __Damping__ is applied, the particles will not slow down or accelerate.
* A value of 0 means particles will stop immediately.
* A value of 2 means particles will double their speed every second.


###Destroying GameObjects attached to Particles

You can destroy the Particle System and any attached __GameObject__ by enabling the __AutoDestruct__ property. For example, if you have an oil drum, you can attach a Particle System that has __Emit__ disabled and __AutoDestruct__ enabled. On collision, you enable the Particle Emitter. The explosion will occur and after it is over, the Particle System and the oil drum will be destroyed and removed from the scene.

Note that automatic destruction takes effect only after some particles have been emitted. The precise rules for when the object is destroyed when __AutoDestruct__ is on:

* If there have been some particles emitted already, but all of them are dead now, _or_
* If the [emitter](class-EllipsoidParticleEmitter) did have __Emit__ on at some point, but now __Emit__ is off.

Hints
-----


* Use the __Color Animation__ to make your particles fade in & out over their lifetime - otherwise, you will get nasty-looking pops.
* Use the __Rotation Axes__ to make whirlpool-like swirly motions.
