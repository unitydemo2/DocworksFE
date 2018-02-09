Fixed Joint
===========


__Fixed Joints__ restricts an object's movement to be dependent upon another object. This is somewhat similar to __Parenting__ but is implemented through physics rather than __Transform__ hierarchy. The best scenarios for using them are when you have objects that you want to easily break apart from each other, or connect two object's movement without parenting.


![](../uploads/Main/Inspector-FixedJoint.png) 


Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Connected Body__ |Optional reference to the Rigidbody that the joint is dependent upon. If not set, the joint connects to the world. |
|__Break Force__ |The force that needs to be applied for this joint to break. |
|__Break Torque__ |The torque that needs to be applied for this joint to break. |
|__Enable Collision__ |When checked, this enables collisions between bodies connected with a joint. |
|__Enable Preprocessing__ | Disabling preprocessing helps to stabilize impossible-to-fulfil configurations. |

Details
-------


There may be scenarios in your game where you want objects to stick together permanently or temporarily. Fixed Joints may be a good __Component__ to use for these scenarios, since you will not have to script a change in your object's hierarchy to achieve the desired effect. The trade-off is that you must use __Rigidbodies__ for any objects that use a Fixed Joint.

For example, if you want to use a "sticky grenade", you can write a script that will detect collision with another Rigidbody (like an enemy), and then create a Fixed Joint that will attach itself to that Rigidbody. Then as the enemy moves around, the joint will keep the grenade stuck to them.


###Breaking joints

You can use the __Break Force__ and __Break Torque__ properties to set limits for the joint's strength. If these are less than infinity, and a force/torque greater than these limits are applied to the object, its Fixed Joint will be destroyed and will no longer be confined by its restraints.


Hints
-----


* You do not need to assign a __Connected Body__ to your joint for it to work.
* Fixed Joints require a Rigidbody.
