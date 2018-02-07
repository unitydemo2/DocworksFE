#Capsule Collider

The __Capsule Collider__ is made of two half-spheres joined together by a cylinder. It is the same shape as the Capsule primitive.


![](../uploads/Main/Inspector-CapsuleCollider.png) 


##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Is Trigger__ |If enabled, this Collider is used for triggering events, and is ignored by the physics engine. |
|__Material__ |Reference to the [Physics Material](class-PhysicMaterial) that determines how this Collider interacts with others. |
|__Center__ |The position of the Collider in the object's local space. |
|__Radius__ |The radius of the Collider's local width. |
|__Height__ |The total height of the Collider. |
|__Direction__ |The axis of the capsule's lengthwise orientation in the object's local space. |


##Details

You can adjust the Capsule Collider's __Radius__ and __Height__ independently of each other. It is used in the [Character Controller](class-CharacterController) and works well for poles, or can be combined with other Colliders for unusual shapes.

![A standard Capsule Collider](../uploads/Main/CapsuleColliderDiagram.svg) 
