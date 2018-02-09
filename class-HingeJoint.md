Hinge Joint
===========


The __Hinge Joint__ groups together two [Rigidbodies](class-Rigidbody), constraining them to move like they are connected by a hinge. It is perfect for doors, but can also be used to model chains, pendulums, etc.


![](../uploads/Main/Inspector-HingeJoint.png) 

Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Connected Body__ |Optional reference to the Rigidbody that the joint is dependent upon. If not set, the joint connects to the world. |
|__Anchor__ |The position of the axis around which the body swings. The position is defined in local space. |
|__Axis__ |The direction of the axis around which the body swings. The direction is defined in local space. |
|__Auto Configure Connected Anchor__ |If this is enabled, then the Connected Anchor position will be calculated automatically to match the global position of the anchor property. This is the default behavior. If this is disabled, you can configure the position of the connected anchor manually.|
|__Connected Anchor__ |Manual configuration of the connected anchor position. |
|__Use Spring__ |Spring makes the Rigidbody reach for a specific angle compared to its connected body. |
|__Spring__ |Properties of the Spring that are used if __Use Spring__ is enabled. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Spring__ |The force the object asserts to move into the position. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Damper__ |The higher this value, the more the object will slow down. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Target Position__ |Target angle of the spring. The spring pulls towards this angle measured in degrees. |
|__Use Motor__ |The motor makes the object spin around. |
|__Motor__ |Properties of the Motor that are used if __Use Motor__ is enabled. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Target Velocity__ |The speed the object tries to attain. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Force__ |The force applied in order to attain the speed. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Free Spin__ |If enabled, the motor is never used to brake the spinning, only accelerate it. |
|__Use Limits__ |If enabled, the angle of the hinge will be restricted within the __Min__ & __Max__ values. |
|__Limits __ |Properties of the Limits that are used if __Use Limits__ is enabled. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Min__ |The lowest angle the rotation can go. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Max__ |The highest angle the rotation can go. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Bounciness__ |How much the object bounces when it hits the minimum or maximum stop limit. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Contact Distance__ | Within the contact distance from the limit contacts will persist in order to avoid jitter.|
|__Break Force__ |The force that needs to be applied for this joint to break. |
|__Break Torque__ |The torque that needs to be applied for this joint to break. |
|__Enable Collision__ |When checked, this enables collisions between bodies connected with a joint. |
|__Enable Preprocessing__ | Disabling preprocessing helps to stabilize impossible-to-fulfil configurations. |

Details
-------


A single Hinge Joint should be applied to a __GameObject__. The hinge will rotate at the point specified by the __Anchor__ property, moving around the specified __Axis__ property. You **do not** need to assign a GameObject to the joint's __Connected Body__ property. You should only assign a GameObject to the __Connected Body__ property if you want the joint's __Transform__ to be dependent on the attached object's Transform.

Think about how the hinge of a door works. The __Axis__ in this case is up, positive along the Y axis. The __Anchor__ is placed somewhere at the intersection between door and wall. You would not need to assign the wall to the __Connected Body__, because the joint will be connected to the world by default.

Now think about a doggy door hinge. The doggy door's __Axis__ would be sideways, positive along the relative X axis. The main door should be assigned as the __Connected Body__, so the doggy door's hinge is dependent on the main door's Rigidbody.


###Chains

Multiple Hinge Joints can also be strung together to create a chain. Add a joint to each link in the chain, and attach the next link as the __Connected Body__.


Hints
-----


* You do not need to assign a __Connected Body__ to your joint for it to work.
* Use __Break Force__ in order to make dynamic damage systems. This is really cool as it allows the player to break a door off its hinge by blasting it with a rocket launcher or running into it with a car.
* The __Spring__, __Motor__, and __Limits__ properties allow you to fine-tune your joint's behaviors.
* Use of __Spring__, __Motor__ are intended to be mutually exclusive.  Using both at the same time leads to unpredictable results.
