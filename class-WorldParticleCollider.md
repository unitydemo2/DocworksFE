World Particle Collider (Legacy)
================================


The __World Particle Collider__ is used to collide particles against other __Colliders__ in the scene.


![](../uploads/Main/Inspector-ParticleCollider.png) 


Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Bounce Factor__ |Particles can be accelerated or slowed down when they collide against other objects. This factor is similar to the __Particle Animator's__ __Damping__ property. |
|__Collision Energy Loss__ |Amount of energy (in seconds) a particle should lose when colliding. If the energy goes below 0, the particle is killed. |
|__Min Kill Velocity__ |If a particle's __Velocity__ drops below __Min Kill Velocity__ because of a collision, it will be eliminated. |
|__Collides with__ |Which [Layers](Layers) the particle will collide against. |
|__Send Collision Message__ |If enabled, every particle sends out a collision message that you can catch through scripting. |


Details
-------


To create a Particle System with Particle Collider:

1. Create a Particle System using __GameObject &gt; Create General &gt; Particle System__
1. Add the Particle Collider using __Component &gt; Particles &gt; World Particle Collider__


###Messaging

If __Send Collision Message__ is enabled, any particles that are in a collision will send the message __OnParticleCollision()__ to both the particle's __GameObject__ and the GameObject the particle collided with.


Hints
-----



* __Send Collision Message__ can be used to simulate bullets and apply damage on impact.
* Particle Collision Detection is slow when used with a lot of particles. Use Particle Collision Detection wisely.
* Message sending introduces a large overhead and shouldn't be used for normal Particle Systems.

![A __Particle System__ colliding with a __Mesh Collider__](../uploads/Main/ParticleColliderScreen.png) 


