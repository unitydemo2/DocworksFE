# Composite Collider 2D

The Composite Collider 2D [component](UsingComponents) is a [Collider](CollidersOverview) for use with 2D physics. Unlike most colliders, it does not define an inherent shape. Instead, it merges the shapes of any [Box Collider 2D](class-BoxCollider2D) or [Polygon Collider 2D](class-PolygonCollider2D) that you set it up to use. The Composite Collider 2D uses the vertices (geometry) from any of these Colliders, and merges them together into new geometry controlled by the Composite Collider 2D itself.

The Box Collider 2D and Polygon Collider 2D components have a __Used By Composite__ checkbox.   Tick this checkbox to attach them to the Composite Collider 2D. These Colliders also have to be attached to the same [Rigidbody 2D](class-Rigidbody2D) as the Composite Collider 2D. When you enable __Used by Composite__, other properties disappear from that component, because they are now controlled by the attached Composite Collider 2D.

See API documentation on [Composite Collider 2D](ScriptRef:CompositeCollider2D.html) for more information about scripting with the Composite Collider 2D. 

![](../uploads/Main/class-CompositeCollider2D.png)

| **Property**| **Function** |
|:---|:---| 
| __Density__ | Change the density to change the mass calculations of the [GameObject’s](GameObjects) associated Rigidbody 2D. If you set the value to 0, its associated Rigidbody 2D ignores the Collider 2D for all mass calculations, including centre of mass calculations. Note that this option is only available if you have enabled __Use Auto Mass__ in the associated Rigidbody 2D component. |
| __Material__ | A [Physics Material 2D](class-PhysicsMaterial2D) that determines the properties of collisions, such as friction and bounce. |
| __Is Trigger__ | Check this box if you want the Composite Collider 2D to behave as a trigger (see overview documentation on [Colliders](CollidersOverview) to learn more about triggers). |
| __Used by Effector__ | Check this box if you want the Composite Collider 2D to be used by an attached [Effector 2D](Effectors2D) component. |
| __Offset__| Set the local offset of the Collider 2D geometry. |
| __Geometry Type__ | When merging Colliders, the vertices from the selected Colliders are composed into one of two different geometry types. Use this drop-down to set the geometry type to either __Outlines__ or __Polygons__.  |
|&nbsp;&nbsp;&nbsp;&nbsp;Outlines| Produces a Collider 2D with hollow outlines, identical to what the [Edge Collider 2D](class-EdgeCollider2D) produces. |
|&nbsp;&nbsp;&nbsp;&nbsp;Polygons| Produces a Collider 2D with solid polygons, identical to what the [Polygon Collider 2D](class-PolygonCollider2D) produces. |
| __Generation Type__ | The method used to control when geometry is generated when either the Composite Collider 2D is changed, or any of the Colliders it is composing is changed. |
|&nbsp;&nbsp;&nbsp;&nbsp;Synchronous| When a change is made to the Composite Collider 2D or any of the colliders it is using, Unity generates new geometry immediately. |
|&nbsp;&nbsp;&nbsp;&nbsp;Manual| New geometry generation happens only when you request it. To request generation, either call the [CompositeCollider2D.GenerateGeometry](ScriptRef:CompositeCollider2D.GenerateGeometry.html) script API, or click the __Regenerate Geometry__ button that appears under the selection. |
| __Vertex Distance__| Set a value for the minimum spacing allowed for any vertices gathered from Colliders being composed. Any vertex closer than this limit is removed. This allows control over the effective resolution of the vertex compositing. |
| __Edge Radius__| Controls a radius around edges, so that vertices are circular. This results in a larger Collider 2D with rounded convex corners. The default value for this setting is 0 (no radius). This only works when the __Geometry Type__ is set to __Outlines__. |