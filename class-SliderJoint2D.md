Slider Joint 2D
================


This joint allows a game object controlled by rigidbody physics to slide along a line in space, like sliding doors, for example. The object can freely move anywhere along the line in response to collisions or forces or, alternatively, it can be moved along by a motor force, with limits applied to keep its position within a certain section of the line.


![](../uploads/Main/SliderJoint2DInspector.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Enable Collision__ |Can the two connected objects collide with each other? Check the box for yes.|
|__Connected Rigid Body__ |Specify here the other object this joint connects to. Leave this as __None__ and the other end of the joint will be fixed at a point in space defined by the __Connected Anchor__ setting. Select the circle to the right of the field to view a list of objects to connect to.|
|__Auto Configure Connected Anchor__ | Check this box to automatically set the anchor location for the other object this joint connects to. (Check this instead of completing the __Connected Anchor__ fields.) |    

|__Anchor__ |The place (in terms of X, Y co-ordinates on the __RigidBody__) where the end point of the joint connects to *this* object. |
|__Connected Anchor__ |The place (in terms of X, Y co-ordinates on the __RigidBody__) where the end point of the joint connects to *the other* object. |
|__Auto Configure Angle__ | Check this box to automtically detect the angle between the two objects and set it as the angle that the joint keeps between the two objects. (By selecting this, you don't need to manually specify the angle.) |
|__Angle__ |Enter the the angle that the joint keeps between the two objects. |
|__Use Motor__ |Use the sliding motor? Check the box for yes.|

|__Motor__ |  |
|__Motor Speed__ |Target motor speed (m/sec). |
|__Maximum Motor Force__ |The maximum force the motor can apply while attempting to reach the target speed. |
|__Use Limits__ |Should there be limits to the linear (straight line) force? Check the box for yes. |
|__Translation Limits__ |  |
|__Lower Translation__ |The minimum distance the  object can be from the connected anchor point. |
|__Upper Translation__ |The maximum distance the  object can be from the connected anchor point. |
|__Break Force__ |Specify the linear (straight line) force level needed to break and so delete the joint. __Infinity__ means it is unbreakable. |
|__Break Torque__ |Specify the torque (rotation) level needed to break and so delete the joint. __Infinity__ means it is unbreakable. |

Details
-------
(See also [Joints 2D](Joints2D): *Details and Hints* for useful background information on all 2D joints.)

Use this joint to make objects slide! The aim of this joint is to maintain the position of two points on a configurable line that extends to infinity. Those two points can be two __Rigidbody2D__ components or a __Rigidbody2D__ component and a fixed position in the world. (Connect to a fixed position in the world by setting __Connected Rigidbody__ to None). 


The joint applies a linear force to both connected rigid body objects to keep them on the line. It also has a simulated linear motor that applies linear force to move the ridid body objects along the line.  You can turn the motor off or on. Athough the line is infinite, you can specify just a segment of the line that you want to use, using the __Translation Limits__ option. 

This joint has three simultaneous constraints. All are optional:

* Maintain a relative linear distance away from a specified line between two anchor points on two rigid body objects.
* Maintain a linear speed between two anchor points on two rigid body objects along a specified line. (The speed is limited with a maximum force.)
* Maintain a linear distance between two points along the specified line.

**For Example:**

You can use this joint to construct physical objects that need to react as if they are connected together on a line.  Such as:

* A platform which can move up or down. The platform reacts by moving down when something lands on it but  must never move sideways.  You can use this joint to ensure platform to never moves up or down beyond certain limits.  Use the motor to make the platform move up. 


