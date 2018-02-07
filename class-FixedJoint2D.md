#Fixed Joint 2D

Apply this component to two GameObjects controlled by Rigidbody 2D physics to keep them in a position relative to each other, so the GameObjects are always offset at a given position and angle. It is a spring-type 2D joint for which you don’t need to set maximum forces. You can set the spring to be rigid or soft.

See *Fixed Joint 2D and Relative Joint 2D* below for more information about the differences between __Fixed Joint 2D__ and __Relative Joint 2D__.


![](../uploads/Main/FixedJoint2DInspector.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Enable Collision__ |Check this box to enable the ability for the two connected GameObjects to collide with each other.|
|__Connected Rigid Body__ |Specify the other GameObject this Fixed Joint 2D connects to. Leave this as __None__ to fix the other end of the Fixed Joint 2D to a point in space defined by the __Connected Anchor__ setting. Select the circle to the right of the field to view a list of GameObjects to connect to.|
|__Auto Configure Connected Anchor__ | Check this box to automatically set the anchor location for the other GameObject this Fixed Joint 2D connects to. If you check this, you don't need to complete the __Connected Anchor__ fields. |    
|__Anchor__ |The place (in terms of x,y co-ordinates on the __Rigidbody 2D__) where the end point of the joint connects to *this* object. |
|__Connected Anchor__ |The place (in terms of x, y co-ordinates on the __Rigidbody 2D__) where the end point of the Fixed Joint 2D connects to the other GameObject. |
|__Damping Ratio__ | Define the degree to which you want to suppress spring oscillation, between 0 and 1, the higher the value, the less movement. |
|__Frequency__ |The frequency at which the spring oscillates while the GameObjects are approaching the separation distance you want, measured in cycles per second. In the range 1 to 1,000,000, the higher the value, the stiffer the spring. Note that if the frequency is set to 0, the spring is completely stiff. |
|__Break Force__ |Specify the force level needed to break and therefore delete the joint. __Infinity__ means it is unbreakable. |
|__Break Torque__ |Specify the torque level needed to break and therefore delete the joint. __Infinity__ means it is unbreakable. |



##Notes

The aim of this joint is to maintain a relative linear and angular offset between two points.  Those two points can be two __Rigidbody 2D__ components or a __Rigidbody 2D__ component and a fixed position in the world. (Connect to a fixed position in the world by setting __Connected Rigidbody__ to None).  

The linear and angular offsets are based upon the relative positions and orientations of the two connected points, so you change the offsets by moving the connected GameObjects in your Scene view.  

The joint applies both linear and torque forces to connected Rigidbody 2D GameObjects. It uses a simulated spring that is pre-configured to be as stiff as the simulation can provide. You can change the spring's value to make it weaker using the __Frequency__ setting.

When the spring applies its force between the GameObjects, it tends to overshoot the desired distance between them and then rebound repeatedly, resulting in a continuous oscillation. The damping ratio determines how quickly the oscillation reduces and brings the GameObjects to rest. The frequency is the rate at which it oscillates either side of the target distance; the higher the frequency, the stiffer the spring.

Fixed Joint 2D has two simultaneous constraints:

* Maintain the linear offset between two anchor points on two Rigidbody 2D GameObjects.
* Maintain the angular offset between two anchor points on two Rigidbody 2D GameObjects.

You can use this joint to construct physical GameObjects that need to react as if they are rigidly connected. They can't move away from each other, they can't move closer together, and they can't rotate with respect to each other, such as a bridge made of sections which hold rigidly together. 

You can also use this joint to create a less rigid connection that flexes - for example, a bridge made of sections which are slightly flexible.


##Fixed Joint 2D and Relative Joint 2D
It is important to know the major differences between Fixed Joint 2D and Relative Joint 2D:

* __Fixed Joint 2D__ is a spring-type joint. __Relative Joint 2D__ is a motor-type joint with a maximum force and/or torque.  
* __Fixed Joint 2D__ uses a spring to maintain the relative linear and angular offsets. __Relative Joint 2D__ uses a motor. You can configure a joint's spring or motor.
* __Fixed Joint 2D__ works with anchor points (it’s derived from script __Anchored Joint 2D__); it  maintains the relative linear and angular offset between the anchors. __Relative Joint 2D__ doesn’t have anchor points (it’s derived directly from script __Joint 2D__).
* __Fixed Joint 2D__ cannot modify the relative linear and angular offsets in real time. __Relative Joint 2D__ can.


See [Joints 2D](Joints2D): *Details and Hints* for useful background information on all 2D joints.



