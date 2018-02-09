#Terrain Collider

The __Terrain Collider__ implements a collision surface with the same shape as the [Terrain](script-Terrain) object it is attached to.

![](../uploads/Main/Inspector-TerrainCollider.png) 


##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Material__ |Reference to the [Physics Material](class-PhysicMaterial) that determines how this Collider interacts with others. |
|__Terrain Data__ |The terrain data. |
|__Enable Tree Colliders__ |When selected Tree Colliders will be enabled. |

##Details

You should note that versions of Unity before 5.0 had a __Smooth Sphere Collisions__ property for the Terrain Collider in order to improve interactions between terrains and spheres. This property is now obsolete since the smooth interaction is standard behaviour for the physics engine and there is no particular advantage in switching it off.