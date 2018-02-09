#Spring Joint

The __Spring Joint__ joins two [Rigidbodies](class-Rigidbody) together but allows the distance between them to change as though they were connected by a spring.

![](../uploads/Main/Inspector-SpringJoint.png) 


##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Connected Body__ |The Rigidbody object that the object with the spring joint is connected to. If no object is assigned then the spring will be connected to a fixed point in space.|
|__Anchor__ |The point in the object's local space at which the joint is attached.|
|__Auto Configure Connected Anchor__ |Should Unity calculate the position of the connected anchor point automatically?  |
|__Connected Anchor__ |The point in the connected object's local space at which the joint is attached. |
|__Spring__ |Strength of the spring.|
|__Damper__ |Amount that the spring is reduced when active. |
|__Min Distance__ |Lower limit of the distance range over which the spring will not apply any force. |
|__Max Distance__ |Upper limit of the distance range over which the spring will not apply any force. |
|__Tolerance__ |Changes error tolerance. Allows the spring to have a different rest length. |
|__Break Force__ |The force that needs to be applied for this joint to break. |
|__Break Torque__ |The torque that needs to be applied for this joint to break. |
|__Enable Collision__ |Should the two connected objects register collisions with each other? |
|__Enable Preprocessing__ | Disabling preprocessing helps to stabilize impossible-to-fulfil configurations. |

##Details

The spring acts like a piece of elastic that tries to pull the two anchor points together to the exact same position. The strength of the pull is proportional to the current distance between the points with the force per unit of distance set by the _Spring_ property. To prevent the spring from oscillating endlessly you can set a _Damper_ value that reduces the spring force in proportion to the relative speed between the two objects. The higher the value, the more quickly the oscillation will die down.

You can set the anchor points manually but if you enable _Auto Configure Connected Anchor_, Unity will set the connected anchor so as to maintain the initial distance between them (ie, the distance you set in the scene view while positioning the objects).

The _Min Distance_ and _Max Distance_ values allow you to set a distance range over which the spring will not apply any force. You could use this, for example, to allow the objects a small amount of independent movement but then pull them together when the distance between them gets too great. 

