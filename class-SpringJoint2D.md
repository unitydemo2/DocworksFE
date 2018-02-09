Spring Joint 2D
===============


The __Spring Joint 2D__ component allows two game objects controlled by rigidbody physics to be attached together as if by a spring. The spring will apply a force along its axis between the two objects, attempting to keep them a certain distance apart.


![](../uploads/Main/SpringJoint2DInspector.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Enable Collision__ |Can the two connected objects collide with each other? Check the box for yes.|
|__Connected Rigid Body__ |Specify here the other object this joint connects to. Leave this as __None__ and the other end of the joint will be fixed at a point in space defined by the __Connected Anchor__ setting. Select the circle to the right of the field to view a list of objects to connect to.|
|__Auto Configure Connected Anchor__ | Check this box to automatically set the anchor location for the other object this joint connects to. (Check this instead of completing the __Connected Anchor__ fields.) |    

|__Anchor__ |The place (in terms of X, Y co-ordinates on the __RigidBody__) where the end point of the joint connects to *this* object. |
|__Connected Anchor__ |The place (in terms of X, Y co-ordinates on the __RigidBody__) where the end point of the joint connects to *the other* object. |
|__Auto Configure Distance__ | Check this box to automtically detect the distance between the two objects and set it as the distance that the joint keeps between the two objects. |
|__Distance__ |The distance that the spring should attempt to maintain between the two objects. (Can be set manually.) |
|__Damping Ratio__ | The degree to which you want to suppress spring oscillation: In the range 0 to 1, the higher the value, the less movement. |
|__Frequency__ |The frequency at which the spring oscillates while the objects are approaching the separation distance you want (measured in cycles per second): In the range 0 to 1,000,000 - the higher the value, the stiffer the spring. |
|__Break Force__ |Specify the force level needed to break and so delete the joint. __Infinity__ means it is unbreakable. |


Details
-------
(See also [Joints 2D](Joints2D): *Details and Hints* for useful background information on all 2D joints.)


This joint behaves like a spring. Its aim is to keep a linear distance between two points. You  set this via the __Distance__ setting. Those two points can be two __Rigidbody2D__ components or a __Rigidbody2D__ component and a fixed position in the world. (Connect to a fixed position in the world by setting __Connected Rigidbody__ to None).  The joint aplies a linear force to both rigid bodies. It doesn't apply torque (an angle force).  

The joint uses a simulated spring. You can set the spring's stiffness and movement:

A stiff, barely moving spring...

* A high (1,000,000 is the highest)  __Frequency__ == a stiff spring.

* A high (1 is the highest) __Damping Ratio__ ==  a barely moving spring.

A loose, moving spring...

* A low  __Frequency__ == a loose spring.

* A low  __Damping Ratio__ ==  a moving spring.

When the spring applies its force between the objects, it tends to overshoot the distance you have set between them, and then rebound repeatedly, giving in a continuous oscillation. The __Damping Ratio__ sets how quickly the objects stop moving. The __Frequency__ sets how quickly the objects oscillate either side of the target distance.

This joint has one constraint:

* Maintain a zero linear distance between two anchor points on two rigid body objects.

**For Example:**

You can use this joint to construct physical objects that need to react as if they are connected together using a spring or a connection which allows rotation.  Such as:

* A character who's body is composed of multiple objects that act as if they are semi-rigid. Use the the Spring Joint to connect the character's body parts together, allowing them to flex to and from each other.  You can specify whether the body parts are held together loosely or tightly.


**HINTS:**

* Zero in the __Frequency__ is a special case: It gives the stiffest spring possible.
* Spring Joint 2D uses a Box 2D spring-joint.
Distance Joint 2D also uses the same Box 2D spring-joint but it sets the frequency to zero!   Technically, a Spring Joint 2D with a frequency of zero and damping of 1 is identical to a Distance Joint 2D!





