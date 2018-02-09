#Friction Joint 2D

The __Friction Joint 2D__ connects GameObjects controlled by Rigidbody 2D physics. The Friction Joint 2D reduces both the linear and angular velocities between the objects to zero (ie, it slows them down).  You can use this joint to simulate top-down friction, for example.

![](../uploads/Main/FrictionJoint2DInspector.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Enable Collision__ |Check the box to enable collisions between the two connected GameObjects.|
|__Connected Rigid Body__ |Specify the other GameObject this Friction Joint 2D connects to. If you leave this as __None__, the other end of the Friction Joint 2D is fixed to a point in space defined by the __Connected Anchor__ setting. Select the circle to the right of the field to view a list of GameObjects to connect to.|
|__Auto Configure Connected Anchor__ | Check this box to automatically set the anchor location for the other GameObject this Friction Joint 2D connects to. If you check this, you don't need to complete the __Connected Anchor__ fields. |    
|__Anchor__ |Define where (in terms of x, y co-ordinates on the __RigidBody 2D__) the end point of the Friction Joint 2D connects to this GameObject. |
|__Connected Anchor__ |Define where (in terms of x, y co-ordinates on the __RigidBody 2D__) the end point of the Friction Joint 2D connects to the other GameObject. |
|__Max Force__ | Sets the linear (or straight line) movement between joined GameObjects. A high value resists the linear movement between GameObjects. |
|__Max Torque__ | Sets the angular (or rotation) movement between joined GameObjects. A high value resists the rotation movement between GameObjects. |
|__Break Force__ |Specify the force level needed to break and therefore delete the Friction Joint 2D. __Infinity__ means it is unbreakable. |
|__Break Torque__ |Specify the torque level needed to break and therefore delete the Friction Joint 2D. __Infinity__ means it is unbreakable. |


##Notes

Use the Friction Joint 2D to slow down movement between two points to a stop. This joint's aim is to maintain a zero relative linear and angular offset between two points. Those two points can be two __Rigidbody 2D__ components or a __Rigidbody 2D__ component and a fixed position in the world. (Connect to a fixed position in the world by setting __Connected Rigidbody__ to None).

###Resistance
The joint applies linear force (__Force__) and angle force (__Torque__) to both Rigidbody 2D points. It uses a simulated motor that is pre-configured to have a low motor power (and so, low resistence). You can change the resistance to make it weaker or stronger.

Strong Resistance: 

* A high (1,000,000 is the highest)  __Max Force__ creates strong linear resistance. The Rigidbody 2D GameObjects won't move in a line relative to each other very much. 
* A high (1,000,000 is the highest) __Max Torque__ creates strong angular resistance. The Rigidbody 2D GameObjects won't move at an angle relative to each each other very much.

Weak Resistance:

* A low __Max Force__  creates  weak linear resistance. The Rigidbody 2D GameObjects move easily in a line relative to each other. 
* A low __Max Torque__ creates weak angular resistance. The Rigidbody 2D GameObjects move easily at an angle relative to each each other.

###Constraints
Friction Joint 2D has two simultaneous constraints:

* Maintain a zero relative linear velocity between two anchor points on two Rigidbody 2Ds
* Maintain a zero relative angular velocity between two anchor points on two Rigidbody 2Ds

You can use this joint to construct physical GameObjects that need to behave as if they have friction. They can resist either linear movement or angular movement, or both linear and angular movement. For example:

* A platform that does rotate, but resists applied forces, making it difficult but possible for the player to move it.
* A ball that resists linear movement. The ball's friction is related to the GameObject's velocity and not to any collisions. It acts like the __Linear Drag__ and __Angular Drag__ which is set in __Rigidbody 2D__. The difference is that Friction Joint 2D has the option of maximum __Force__ and __Torque__ settings.)

See [Joints 2D](Joints2D): *Details and Hints* for useful background information on all 2D joints.

