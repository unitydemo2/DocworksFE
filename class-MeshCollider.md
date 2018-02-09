#Mesh Collider

The __Mesh Collider__ takes a [Mesh Asset](class-Mesh) and builds its Collider based on that Mesh. It is far more accurate for collision detection than using primitives for complicated Meshes. Mesh Colliders that are marked as __Convex__ can collide with other Mesh Colliders.


![](../uploads/Main/Inspector-MeshCollider.png) 


##Properties

|**_Property_** |**_Function_** |
|:---|:---|
|__Is Trigger__ |If enabled, this Collider is used for triggering events, and is ignored by the physics engine. |
|__Material__ |Reference to the [Physics Material](class-PhysicMaterial) that determines how this Collider interacts with others. |
|__Mesh__ |Reference to the Mesh to use for collisions. |
|__Convex__ |Tick the checkbox to enable __Convex__. If enabled, this Mesh Collider collides with other Mesh Colliders. __Convex__ Mesh Colliders are limited to 255 triangles. |


##Details

The Mesh Collider builds its collision representation from the [Mesh](class-Mesh) attached to the GameObject, and reads the properties of the attached [Transform](class-Transform) to set its position and scale correctly. The benefit of this is that you can make the shape of the Collider exactly the same as the shape of the visible Mesh for the GameObject, resulting in more precise and authentic collisions. However, this precision comes with a higher processing overhead than collisions involving primitive colliders (such as Sphere, Box, and Capsule) and so it is best to use Mesh Colliders sparingly.

Faces in collision meshes are one-sided. This means objects can pass through them from one direction, but collide with them from the other.

There are some limitations when using the Mesh Collider:

* Mesh Colliders that do not have __Convex__ enabled are only supported on GameObjects without a Rigidbody component. To apply a Mesh Collider to a Rigidbody component, tick the __Convex__ checkbox.
* In certain cases, for a Mesh Collider to work properly, you need to tick the __Read/Write Enabled__ checkbox in the Mesh [Import Settings](ImportSettings). These cases include:
    * Negative scaling (for example, (-1, 1, 1)).
    * Shear transform (for example, when a rotated Mesh has a scaled parent transform).

__Optimization tip:__ If a Mesh is used only by a Mesh Collider, you can disable __Normals__ in __Import Settings__, because the physics system doesn’t need them.

Note that versions of Unity before 5.0 had a __Smooth Sphere Collisions__ property for the Mesh Collider in order to improve interactions between meshes and spheres. This property is now obsolete because the smooth interaction is standard behaviour for the physics engine, and there is no particular advantage in switching it off.