#Hinge Joint 2D

The __Hinge Joint 2D__ component allows a GameObject controlled by RigidBody 2D physics to be attached to a point in space around which it can rotate. The rotation can be left to happen passively (for example, in response to a collision) or can be actively powered by a motor torque provided by the Joint 2D itself. You can set limits to prevent the hinge from making a full rotation, or make more than a single rotation.

##Properties

![](../uploads/Main/HingeJoint2DInspector.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Enable Collision__ |Check the box to enable collisions between the two connected GameObjects.|
|__Connected Rigid Body__ |Specify the other GameObject this Hinge Joint 2D connects to. If you leave this as __None__, the other end of the Hinge Joint 2D is fixed to a point in space defined by the __Connected Anchor__ setting. Select the circle to the right of the field to view a list of GameObjects to connect to.|
|__Auto Configure Connected Anchor__ | Check this box to automatically set the anchor location for the other GameObject this Hinge Joint 2D connects to. If you check this, you don't need to complete the __Connected Anchor__ fields. |    
|__Anchor__ |Define where (in terms of x, y co-ordinates on the __RigidBody 2D__) the end point of the Friction Joint 2D connects to this GameObject. |
|__Connected Anchor__ |Define where (in terms of x, y co-ordinates on the __RigidBody 2D__) the end point of the Friction Joint 2D connects to the other GameObject. |
|__Motor__|Use this to change Motor settings.|
|__Use Motor__ |Check the box to enable the hinge motor. |
|__Motor Speed__ |Set the target motor speed, in degrees per second. |
|__Maximum Motor Force__ |Set the maximum torque (or rotation) the motor can apply while attempting to reach the target speed. |
|__Use Limits__ |Check this box to limit the rotation angle |
|__Angle Limits__ | Use these settings to set limits if __Use Limits__ is enabled. |
|__Lower Angle__ |Set the lower end of the rotation arc allowed by the limit. |
|__Upper Angle__ |Set the upper end of the rotation arc allowed by the limit. |
|__Break Force__ |Specify the linear (or straight line) force level needed to break and therefore delete the joint. __Infinity__ means it is unbreakable. |
|__Break Torque__ |Specify the the angular (or rotation) level needed to break and therefore delete the joint. __Infinity__ means it is unbreakable. |


##Notes

The Hinge Joint 2D's name suggest a door hinge. It can be used as a door hinge, but also anything that rotates around a particular point - for example: machine parts, powered wheels, and pendulums.

You can use this joint to make two points overlap. Those two points can be two __Rigidbody 2D__ components, or a __Rigidbody 2D__ component and a fixed position in the world. Connect the Hinge Joint 2D to a fixed position in the world by setting __Connected Rigid Body__ to None. The joint applies a linear force to both connected Rigidbody 2D GameObjects.

The Hinge Joint 2D has a simulated rotational motor which you can turn on or off. Set the __Maximum Motor Speed__ and __Maximum Motor Force__ to control the angular speed (__Torque__) and make the two Rigidbody 2D GameObjects rotate in an arc relative to each other. Set the limits of the arc using __Lower Angle__ and __Upper Angle__.

###Constraints

Hinge Joint 2D has three simultaneous constraints. All are optional:

* Maintain a relative linear distance between two anchor points on two Rigidbody 2D GameObjects.
* Maintain an angular speed between two anchor points on two Rigidbody 2D GameObjects (limited with a maximum torque in __Maximum Motor Force __.
* Maintain an angle within a specified arc.

You can use this joint to construct physical GameObjects that need to behave as if they are connected with a rotational pivot. For example: 

* A see-saw pivot where the horizontal section is connected to the base. Use the joint's __Angle Limits__ to simulate the highest and lowest point of the see-saw's movement.
* A pair of scissors connected together with a hinge pivot. Use the joint's __Angle Limits__ to simulate the closing and maximum opening of the scisssors.
* A simple wheel connected to the body of a car with the pivot connecting the wheel at its center to the car. In this example you can use the Hinge Joint 2D's motor to rotate the wheel.

See [Joints 2D](Joints2D): *Details and Hints* for useful background information on all 2D joints.
