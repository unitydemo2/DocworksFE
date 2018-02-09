Target Joint 2D
================

This joint connects to a specified target, rather than another rigid body object, as other joints do. It is a spring type joint, which you could use for picking up and moving an object acting under gravity, for example.


![](../uploads/Main/TargetJoint2DInspector.png) 




|**_Property:_** |**_Function:_** |
|:---|:---|
|__Anchor__ |The place (in terms of X, Y co-ordinates on the __RigidBody__) where the end point of the joint connects to this object. |
|__Target__ |The place (in terms of X, Y co-ordinates in the world space) towards which the other end of the joint attempts to move.|
|__Auto Configure Target__ | Check this box to automatically set the other end of the joint to the current position of the object. (This option is useful when you are moving the object around, as it sets the initial target position as the current position.) **Note** that when this option is selected, the target changes as you move the object; it won't change if the option is unselected.|
__Max Force__ | Sets the force that the joint can apply when attempting to move the object to the target position. The higher the value, the higher the maximum force.  |
|__Damping Ratio__ | The degree to which you want to suppress spring oscillation: In the range 0 to 1, the higher the value, the less movement. |
|__Frequency__ |The frequency at which the spring oscillates while the objects are approaching the separation distance you want (measured in cycles per second): In the range 0 to 1,000,000 -, the higher the value, the stiffer the spring. |
|__Break Force__ |Specify the force level needed to break and so delete the joint. __Infinity__ means it is unbreakable. |



Details
-------
(See also [Joints 2D](Joints2D): *Details and Hints* for useful background information on all 2D joints.)

Use this joint to connect a rigid body game object to a point in space.

The aim of this joint is to keep zero linear distance between two points: An anchor point on a rigid body object and a world-space position, called the "__Target__".  The joint applies linear force to the rigid body object, it does not apply torque (anglular force). 

The joint uses a simulated spring. You can set the spring's stiffness and movement:

A stiff, barely moving spring...

* A high (1,000,000 is the highest)  __Frequency__ == a stiff spring.

* A high (1 is the highest) __Damping Ratio__ ==  a barely moving spring.

A loose, moving spring...

* A low  __Frequency__ == a loose spring.

* A low __Damping Ratio__ ==  a moving spring.

When the spring applies its force between the  rigid body object and target, it tends to overshoot the distance you have set between them, and then rebound repeatedly, giving in a continuous oscillation. The __Damping Ratio__ sets how quickly the rigid body object stops moving. The __Frequency__ sets how quickly the rigid body object oscillates either side of the distance you have specified.

This joint has one constraint:

* Maintain a zero linear distance between the anchor point on a rigid body object and a world-space position (__Target__).

**For Example:**

You can use this joint to construct physical objects that need to move to designated target positions and stay there until another target position is selected or the turned-off.  Such as:

* A game where players pick up cakes, using a mouse-click, and drag them into to a plate.  You can use this joint to move each cake to the plate.  

You could also use the joint to allow objects to hang: If the anchor point is not the center of mass, then the object will rotate. Such as:

* A game where players pick up boxes. If they use a mouse-click to pick a box up by its corner and drag it, it will hang from the cursor.

**HINT:**

* Zero in the __Frequency__ is a special case: It gives the stiffest spring possible.



