#Sphere Collider

The __Sphere Collider__ is a basic sphere-shaped collision primitive.

![](../uploads/Main/Inspector-SphereCollider.png) 


##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Is Trigger__ |If enabled, this Collider is used for triggering events, and is ignored by the physics engine. |
|__Material__ |Reference to the [Physics Material](class-PhysicMaterial) that determines how this Collider interacts with others. |
|__Center__ |The position of the Collider in the object's local space. |
|__Radius__ |The size of the Collider. |


##Details

The collider can be resized via the __Radius__ property but cannot be scaled along the three axes independently (ie, you can't flatten the sphere into an ellipse). As well as the obvious use for spherical objects like tennis balls, etc, the sphere also works well for falling boulders and other objects that need to roll and tumble.