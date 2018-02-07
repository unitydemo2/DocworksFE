#Collider combinations

There are numerous different combinations of collisions that can happen in Unity. Each game is unique, and different combinations may work better for different types of games. If you're using physics in your game, it will be very helpful to understand the different basic Collider types, their common uses, and how they interact with other types of objects.

###Static Collider
These are GameObjects that do not have a Rigidbody attached, but do have a Collider attached. These objects should remain still, or move very little. These work great for your environment geometry. They will not move if a Rigidbody collides with them.

###Rigidbody Collider
These GameObjects contain both a Rigidbody and a Collider. They are completely affected by the physics engine through scripted forces and collisions. They might collide with a GameObject that only contains a Collider. These will likely be your primary type of Collider in games that use physics.

###Kinematic Rigidbody Collider
This GameObject contains a Collider and a Rigidbody which is marked **IsKinematic**. To move this GameObject, you modify its Transform Component, rather than applying forces. They're similar to Static Colliders but will work better when you want to move the Collider around frequently. There are some other specialized scenarios for using this GameObject.

This object can be used for circumstances in which you would normally want a Static Collider to send a trigger event. Since a Trigger must have a Rigidbody attached, you should add a Rigidbody, then enable **IsKinematic**. This will prevent your Object from moving from physics influence, and allow you to receive trigger events when you want to.

Kinematic Rigidbodies can easily be turned on and off. This is great for creating ragdolls, when you normally want a character to follow an animation, then turn into a ragdoll when a collision occurs, prompted by an explosion or anything else you choose. When this happens, simply turn all your Kinematic Rigidbodies into normal Rigidbodies through scripting.

If you have Rigidbodies come to rest so they are not moving for some time, they will "fall asleep". That is, they will not be calculated during the physics update since they are not going anywhere. If you move a Kinematic Rigidbody out from underneath normal Rigidbodies that are at rest on top of it, the sleeping Rigidbodies will "wake up" and be correctly calculated again in the physics update. So if you have a lot of Static Colliders that you want to move around and have different object fall on them correctly, use Kinematic Rigidbody Colliders.

##Collision action matrix

Depending on the configurations of the two colliding Objects, a number of different actions can occur. The chart below outlines what you can expect from two colliding Objects, based on the components that are attached to them. Some of the combinations only cause one of the two Objects to be affected by the collision, so keep the standard rule in mind - physics will not be applied to objects that do not have Rigidbodies attached.

|**_Collision detection occurs and messages are sent upon collision_** |||||||
|:---|:---|:---|:---|:---|:---|:---|
||Static Collider|Rigidbody Collider|Kinematic Rigidbody Collider|Static Trigger Collider|Rigidbody Trigger Collider|Kinematic Rigidbody Trigger Collider|
|Static Collider|&nbsp;|Y|&nbsp;|&nbsp;|&nbsp;|&nbsp;|
|Rigidbody Collider|Y|Y|Y|&nbsp;|&nbsp;|&nbsp;|
|Kinematic Rigidbody Collider|&nbsp;|Y|&nbsp;|&nbsp;|&nbsp;|&nbsp;|
|Static Trigger Collider|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|
|Rigidbody Trigger Collider|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|
|Kinematic Rigidbody Trigger Collider|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

|**_Trigger messages are sent upon collision_** |||||||
|:---|:---|:---|:---|:---|:---|:---|
||Static Collider|Rigidbody Collider|Kinematic Rigidbody Collider|Static Trigger Collider|Rigidbody Trigger Collider|Kinematic Rigidbody Trigger Collider|
|Static Collider|&nbsp;|&nbsp;|&nbsp;|&nbsp;|Y|Y|
|Rigidbody Collider|&nbsp;|&nbsp;|&nbsp;|Y|Y|Y|
|Kinematic Rigidbody Collider|&nbsp;|&nbsp;|&nbsp;|Y|Y|Y|
|Static Trigger Collider|&nbsp;|Y|Y|&nbsp;|Y|Y|
|Rigidbody Trigger Collider|Y|Y|Y|Y|Y|Y|
|Kinematic Rigidbody Trigger Collider|Y|Y|Y|Y|Y|Y|