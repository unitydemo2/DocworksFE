#Ellipsoid Particle Emitter (Legacy)


The __Ellipsoid Particle Emitter__ spawns particles inside a sphere. Use the __Ellipsoid__ property below to scale & stretch the sphere.


![](../uploads/Main/Inspector-EllipsoidEmitter.png) 


##Properties


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Emit__ |If enabled, the emitter will emit particles. |
|__Min Size__ |The minimum size each particle can be at the time when it is spawned. |
|__Max Size__ |The maximum size each particle can be at the time when it is spawned. |
|__Min Energy__ |The minimum lifetime of each particle, measured in seconds. |
|__Max Energy__ |The maximum lifetime of each particle, measured in seconds. |
|__Min Emission__ |The minimum number of particles that will be spawned every second. |
|__Max Emission__ |The maximum number of particles that will be spawned every second. |
|__World Velocity__ |The starting speed of particles in world space, along X, Y, and Z. |
|__Local Velocity__ |The starting speed of particles along X, Y, and Z, measured in the object's orientation. |
|__Rnd Velocity__ |A random speed along X, Y, and Z that is added to the velocity. |
|__Emitter Velocity Scale__ |The amount of the emitter's speed that the particles inherit. |
|__Tangent Velocity__ |The starting speed of particles along X, Y, and Z, across the Emitter's surface. |
|__Angular Velocity__ |The angular velocity of new particles in degrees per second.|
|__Rnd Angular Velocity__ |A random angular velocity modifier for new particles.|
|__Rnd Rotation__ |If enabled, the particles will be spawned with random rotations.|
|__Simulate In World Space__ |If enabled, the particles don't move when the emitter moves. If false, when you move the emitter, the particles follow it around. |
|__One Shot__ |If enabled, the particle numbers specified by min & max emission is spawned all at once. If disabled, the particles are generated in a long stream. |
|__Ellipsoid__ |Scale of the sphere along X, Y, and Z that the particles are spawned inside. |
|__MinEmitterRange__ |Determines an empty area in the center of the sphere - use this to make particles appear on the edge of the sphere. |


##Details

Ellipsoid Particle Emitters (EPEs) are the basic emitter, and are included when you choose to add a __Particle System__ to your scene from __Components-&gt;Particles-&gt;Particle System__. You can define the boundaries for the particles to be spawned, and give the particles an initial velocity. From here, use the [Particle Animator](class-ParticleAnimator) to manipulate how your particles will change over time to achieve interesting effects.

Particle Emitters work in conjunction with [Particle Animators](class-ParticleAnimator) and [Particle Renderers](class-ParticleRenderer) to create, manipulate, and display Particle Systems. All three Components must be present on an object before the particles will behave correctly. When particles are being emitted, all different velocities are added together to create the final velocity.


###Spawning Properties

Spawning properties like __Size__, __Energy__, __Emission__, and __Velocity__ will give your particle system distinct personality when trying to achieve different effects. Having a small __Size__ could simulate fireflies or stars in the sky. A large __Size__ could simulate dust clouds in a musky old building.

__Energy__ and __Emission__ will control how long your particles remain onscreen and how many particles can appear at any one time. For example, a rocket might have high __Emission__ to simulate density of smoke, and high __Energy__ to simulate the slow dispersion of smoke into the air.

__Velocity__ will control how your particles move. You might want to change your __Velocity__ in scripting to achieve interesting effects, or if you want to simulate a constant effect like wind, set your X and Z __Velocity__ to make your particles blow away.


###Simulate in World Space

If this is disabled, the position of each individual particle will always translate relative to the __Position__ of the emitter. When the emitter moves, the particles will move along with it. If you have __Simulate in World Space__ enabled, particles will not be affected by the translation of the emitter. For example, if you have a fireball that is spurting flames that rise, the flames will be spawned and float up in space as the fireball gets further away. If __Simulate in World Space__ is disabled, those same flames will move across the screen along with the fireball.


###Emitter Velocity Scale

This property will only apply if __Simulate in World Space__ is enabled.

If this property is set to 1, the particles will inherit the exact translation of the emitter at the time they are spawned. If it is set to 2, the particles will inherit double the emitter's translation when they are spawned. 3 is triple the translation, etc.


###One Shot

__One Shot__ emitters will create all particles within the __Emission__ property all at once, and cease to emit particles over time. Here are some examples of different particle system uses with __One Shot__ __Enabled__ or __Disabled__:

__Enabled__:

* Explosion
* Water splash
* Magic spell

__Disabled__:

* Gun barrel smoke
* Wind effect
* Waterfall



###Min Emitter Range

The __Min Emitter Range__ determines the depth within the ellipsoid that particles can be spawned. Setting it to 0 will allow particles to spawn anywhere from the center core of the ellipsoid to the outer-most range. Setting it to 1 will restrict spawn locations to the outer-most range of the ellipsoid.


![Min Emitter Range of 0](../uploads/Main/EmitterRange0.png) 


![Min Emitter Range of 1](../uploads/Main/EmitterRange1.png) 

##Hints

* Be careful of using many large particles. This can seriously hinder performance on low-level machines. Always try to use the minimum number of particles to attain an effect.
* The __Emit__ property works in conjunction with the __AutoDestruct__ property of the Particle Animator. Through scripting, you can cease the emitter from emitting, and then __AutoDestruct__ will automatically destroy the Particle System and the GameObject it is attached to.

