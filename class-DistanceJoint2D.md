#Distance Joint 2D

__Distance Joint 2D__ is a 2D joint that attaches two GameObjects controlled by __Rigidbody 2D__ physics, and keeps them a certain distance apart. 


![](../uploads/Main/DistanceJoint2DInspector.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Enable Collision__ |Check this box to enable collision between the two connected GameObjects. |
|__Connected Rigid Body__ |Use this field to specify the other GameObject that this Distance Joint 2D connects to. If ths is left as __None (Rigidbody 2D)__, the other end of the Distance Joint 2D is fixed at a point in space defined by the __Connected Anchor__ setting. Select the circle to the right of the field to view a list of GameObjects to connect to.|
|__Auto Configure Connected Anchor__ | Check this box to automatically set the anchor location for the other GameObject this Distance Joint 2D connects to. If you enable this, you don't need to complete the __Connected Anchor__ fields. |
|__Anchor__ |Define where (in terms of x, y co-ordinates on the __Rigidbody 2D__) the end point of the Distance Joint 2D connects to this GameObject. |
|__Connected Anchor__ |Define where (in terms of x, y co-ordinates on the __Rigidbody 2D__) the end point of the Distance Joint 2D connects to the other GameObject. |
|__Auto Configure Distance__ |Check this box to automatically detect the current distance between the two GameObjects, and set it as the distance that the Distance Joint 2D keeps between the two GameObjects. If you enable this, you don't need to complete the __Distance__ field. |
|__Distance__ |Specify the distance that the Distance Joint 2D keeps between the two GameObjects. |
|__Max Distance Only__ |If enabled, the Distance Joint 2D only enforces a maximum distance, so the connected GameObjects can still move closer to each other, but not further than the __Distance__ field defines. If this is not enabled, the distance between the GameObjects is fixed. |
|__Break Force__ |Specify the force level needed to break and therefore delete the Distance Joint 2D. __Infinity__ means it is unbreakable. |


##Notes

The aim of this Joint 2D is to keep distance between two points. Those two points can be two Rigidbody 2D components or a Rigidbody 2D component and a fixed position in the world. 
To connect a __Rigidbody 2D__ component to a fixed position in the world, set the __Connected Rigidbody__ field to None. 

This Joint 2D does not apply torque, or rotation. It does apply a linear force to both connected items, using a very stiff, simulated spring to maintain the distance. You cannot configure the spring.  


This Joint 2D has a selectable constraint:

* Constraint A: Maintains a fixed distance between two anchor points on two bodies (when __Max Distance Only__ is unchecked).
* Constraint B: Maintains maximum distance only between two anchor points on two bodies (when __Max Distance Only__ is checked).

You can use this Joint 2D to construct physical objects that need to behave as if they are connected with a rigid connection that can rotate.

* Using constraint A (__Max Distance Only__ unchecked), you can create a fixed length connection, such as two wheels on a bicycle. 
* Using constraint B (__Max Distance Only__ checked), you can create a constrained length connection, such as a yo-yo moving towards and away from a hand.

See [Joints 2D](Joints2D): *Details and Hints* for useful background information on all 2D Joints.