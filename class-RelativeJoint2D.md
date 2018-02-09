Relative Joint 2D
=================

This joint component allows two game objects controlled by rigidbody physics to maintain in a position based on each other's location. Use this joint to keep two objects offset from each other, at a position and angle you decide. 

See *Details* below for more information about the differences between __RelativeJoint2D__ and __FixedJoint2D__.



![](../uploads/Main/RelativeJoint2DInspector.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Enable Collision__ |Can the two connected objects collide with each other? Check the box for yes.|
|__Connected Rigid Body__ |Specify here the other object this joint connects to. Leave this as __None__ and the other end of the joint will be fixed at a point in space. Select the circle to the right of the field to view a list of objects to connect to.|
|__Max Force__ | Sets the linear (straight line) offset between joined objects - a high value (of up to 1,000) uses high force to maintain the offset. |
|__Max Torque__ | Sets the angular (rotation) movement between joined objects - a high value (of up to 1,000) uses high force to maintain the offset. |
|__Correction Scale__ | Tweaks the joint to make sure it behaves as required. (Increasing the Max Force or Max Torque may affect behaviour so that the joint doesn't reach its target, use this setting to correct it.) The default setting of 0.3 is usually appropriate but it may need tweaking between the range of 0 and 1.  |
|__Auto Configure Offset__ | Check this box to automatically set and maintain the distance and angle between the connected objects. (Selecting this option means you don't need to manually enter the __Linear Offset__ and __Angular Offset__.)   |
|__Linear Offset__ |Enter local space co-ordinates to specify and maintain the distance between the connected objects.|
|__Angular Offset__ |Enter local space co-ordinates to specify and maintain the angle between the connected objects.|
|__Break Force__ |Specify the force level needed to break and so delete the joint. __Infinity__ means it is unbreakable. |
|__Break Torque__ |Specify the torque level needed to break and so delete the joint. __Infinity__ means it is unbreakable. |

##Details
(See also [Joints 2D](Joints2D): *Details and Hints* for useful background information on all 2D joints.)

The aim of this joint is to maintain a relative linear and angular distance (offset) between two points.  Those two points can be two __Rigidbody2D__ components or a __Rigidbody2D__ component and a fixed position in the world. (Connect to a fixed position in the world by setting __Connected Rigidbody__ to None). 

The joint applies a linear  and angular (torque) force to both connected rigid body objects. It uses a simulated motor that is pre-configured to be quite powerful: It has a high __Max Force__ and __Max Torque__ limit. You can lower these values to make the motor less powerful motor or turn-off it off completely.

This joint has two simultaneous constraints:

* Maintain the specified linear offset between the two rigid body objects.
* Maintain the starting angular offset between the two rigid body objects.

**For Example:**

You can use this joint to construct physical objects that need to:

* Keep a distance apart from each other,  as if they are unable to move further away from each other or closer together. (You decide the distance they are apart from each other. The distance can change in real-time.)
* Rotate with respect to each other only at particular angle. (You decide the angle.)

Some uses may need the connection to be flexible, such as: A space-shooter game where the player has extra gun batteries that follow them. You can use the Relative Joint to give the trailing gun batteries a slight lag when they follow, but make them rotate with the player with no lag. 

Some uses may need a configurable force, such as:  A game where the the camera follows a player using a configurable force to keep track.


##Fixed vs. Relative Joint

__FixedJoint2D__ is spring type joint.  __RelativeJoint2D__ is a motor type joint with a maximum force and/or torque.   

* The Fixed Joint uses a spring to maintain the relative linear and angular offsets and the Relative joint uses a motor. You can configure a joint's spring or motor.
* The Fixed joint works with anchor points (it’s derived from script __AnchoredJoint2D__): It  maintains the relative linear and angular offset between the anchors. The Relative joint doesn’t have anchor points (it’s derived directly from script __Joint2D__).
* The Relative joint can modify the relative linear and angular offsets in real time: The Fixed joint cannot.






