#Box Collider

The __Box Collider__ is a basic cube-shaped collision primitive.


![](../uploads/Main/Inspector-BoxCollider.png) 


##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Is Trigger__ |If enabled, this Collider is used for triggering events, and is ignored by the physics engine. |
|__Material__ |Reference to the [Physics Material](class-PhysicMaterial) that determines how this Collider interacts with others. |
|__Center__ |The position of the Collider in the object's local space. |
|__Size__ |The size of the Collider in the X, Y, Z directions. |


##Details

Box colliders are obviously useful for anything roughly box-shaped, such as a crate or a chest. However, you can use a thin box as a floor, wall or ramp. The box shape is also a useful element in a compound collider.