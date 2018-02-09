#Physics 2D Settings


The __Physics 2D Settings__ allow you to provide global settings for 2D physics (menu: __Edit__ > __Project Settings__ > __Physics 2D__). 

(There is also a corresponding [Physics Manager](class-PhysicsManager) for 3D projects.)

![](../uploads/Main/Physics2DManager.png) 

##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Gravity__ |The amount of gravity applied to all [Rigidbody 2D](class-Rigidbody2D) GameObjects. Generally, gravity is only set for the negative direction of the y-axis. |
|__Default Material__ |The default [Physics Material 2D](class-PhysicsMaterial2D) that is used if none has been assigned to an individual Collider 2D. |
|__Velocity Iterations__ |The number of iterations made by the physics engine to resolve velocity effects. Higher numbers result in more accurate physics but at the cost of CPU time. |
|__Position Iterations__ |The number of iterations made by the physics engine to resolve position changes. Higher numbers result in more accurate physics but at the cost of CPU time. |
|__Velocity Threshold__ |Collisions with a relative velocity lower than this value is treated as inelastic collisions (that is, the colliding GameObjects do not bounce off each other). |
|__Max Linear Correction__ |The maximum linear position correction used when solving constraints (from a range between 0.0001 to 1000000). This helps to prevent overshoot. |
|__Max Angular Correction__ |The maximum angular correction used when solving constraints (froma range between 0.0001 to 1000000). This helps to prevent overshoot. |
|__Max Translation Speed__ |The maximum linear speed of a Rigidbody 2D GameObject during any physics update. |
|__Max Rotation Speed__ |The maximum linear speed of a Rigidbody 2D GameObject during any physics update. |
|__Min Penetration For Penalty__ |The minimum contact penetration radius allowed before any separation impulse force is applied. |
|__Baumgarte Scale__ |Scale factor that determines how fast collision overlaps are resolved. |
|__Baumgarte Time of Impact Scale__ |Scale factor that determines how fast time-of-impact overlaps are resolved.  |
|__Time to Sleep__ |The time (in seconds) that must pass after a Rigidbody 2D stops moving before it goes to sleep. |
|__Linear Sleep Tolerance__ |The linear speed below which a Rigidbody 2D goes to sleep after the __Time to Sleep__ elapses. |
|__Angular Sleep Tolerance__ |The rotational speed below which a Rigidbody 2D goes to sleep after __Time to Sleep__ elapses. |
|__Queries Hit Triggers__ |Check this box to enable Collider 2Ds marked as __Triggers__ to return a hit when any physics queries (such as Linecasts or Raycasts) intersect with them. Leave it unchecked for these queries to not return a hit. |
|__Queries Start In Colliders__ | Check this box to enable physics queries that start inside a Collider 2D to detect the collider they start in. |
|__Change Stops Callbacks__ |Check this box to stop reporting collision callbacks immediately if any of the GameObjects involved in the collision are deleted or moved. |
|__Layer Collision Matrix__ |Defines how the [Layer-based collision](LayerBasedCollision) detection system behaves.|

##Notes

The Physics 2D Settings define limits on the accuracy of the physical simulation. Generally speaking, a more accurate simulation requires more processing overhead, so these settings offer a way to trade off accuracy against performance. See the [Physics](PhysicsSection) section of the manual for further information.