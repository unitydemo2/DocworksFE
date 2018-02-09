#Edge Collider 2D

The __Edge Collider 2D__ component is a Collider for use with 2D physics. The Collider's shape is defined by a freeform edge made of line segments, so you can adjust it to fit the shape of the Sprite graphic with great precision. Note that this Collider's edge need not completely enclose an area (unlike the similar [Polygon Collider 2D](class-PolygonCollider2D)), and for example can be a straight line or an L-shape.

![](../uploads/Main/EdgeCollider2DInspector.png) 

|**_Property_** |**_Function_** |
|:---|:---|
|__Density__ |Changing the density here affects the mass of the object's associated Rigidbody. Set the value to __0__ and its associated Rigidbody ignores the Collider for all mass calculations, including center of mass calculations.  **Note:** This option is only available if you have selected __Use Auto Mass__ in an associated Rigidbody.  |
|__Material__ |A physics material that determines properties of collisions, such as friction and bounce. |
|__Is Trigger__ |Tick this box if you want the Collider to behave as a trigger. |
|__Used by Effector__ |Whether the Collider is used by an attached effector or not. |
|__Offset__ |The local offset of the Collider geometry. |
| __Edge Radius__| Controls a radius around edges, so that vertices are circular. This results in a larger [Collider 2D](Collider2D) with rounded convex corners. The default value for this setting is __0__ (no radius).|
|__Points__ |Non-editable information about the complexity of the generated collider. |

##Details

To edit the polyline directly, hold down the Shift key while you move the mouse over an edge or vertex in the Scene view. To move an existing vertex, hold down the Shift key and drag that vertex. To create a new vertex, hold down the Shift key and click where you want the vertex to be created. To remove a vertex, hold down the Ctrl (Windows) or Cmd (macOS) key and click on it.

To hide the outline of the 2D move Gizmo while editing the Collider, click the fold-out arrow on the Sprite Renderer component in the Inspector to collapse it.