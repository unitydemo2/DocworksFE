#Polygon Collider 2D

The __Polygon Collider 2D__ component is a Collider for use with 2D physics. The Collider's shape is defined by a freeform edge made of line segments, so you can adjust it to fit the shape of the Sprite graphic with great precision. Note that this Collider's edge must completely enclose an area (unlike the similar [Edge Collider 2D](class-EdgeCollider2D)).

![](../uploads/Main/PolygonCollider2DInspector.png) 

|**_Property_** |**_Function_** |
|:---|:---|
|__Material__ |A physics material that determines properties of collisions, such as friction and bounce. |
|__Is Trigger__ |Tick this box if you want the Collider to behave as a trigger. |
|__Used by Effector__ |Whether the Collider is used by an attached effector or not. |
| __Used by Composite__ | Tick this checkbox if you want this Collider to be used by an attached [Composite Collider 2D](class-CompositeCollider2D). <br/><br/>When you enable __Used by Composite__, other properties disappear from the Polygon Collider 2D component, because they are now controlled by the attached Composite Collider 2D. The properties that disappear from the Box Collider 2D are __Material__, __Is Trigger__, __Used By Effector__, and __Edge Radius__. |
|__Used by Collider__ | Check this box if you want the Box Collider 2D to be used by an attached [Composite Collider 2D](ScriptRef:CompositeCollider2D.html) component. |
|__Auto Tiling__ | Tick this checkbox if you have set the __Draw Mode__ of the Sprite Renderer component to __Tiled__. This enables automatic updates to the shape of the Collider 2D, meaning that the shape is automatically readjusted when the Sprite’s dimensions change. If you don’t enable __Auto Tiling__, the Collider 2D stays the same shape and size, even when the Sprite’s dimensions change. |
|__Offset__ |The local offset of the Collider geometry. |
|__Points__ |Non-editable information about the complexity of the generated Collider. |


##Details

The Collider can be edited manually but it is often more convenient to let Unity determine the shape automatically. You can do this by dragging a Sprite Asset from the Project view onto the Polygon Collider 2D component in the Inspector.

You can edit the polygon's shape by pressing the __Edit Collider__ button in the Inspector. You can exit Collider edit mode by pressing the __Edit Collider__ button again. While in edit mode, you can move an existing vertex by dragging when the mouse is over that vertex. If you shift-drag while the mouse is over an edge, a new vertex will be created at the mouse location. You can remove a vertex by holding down the ctrl/cmd key while clicking on it.

Note that you can hide the outline of the 2D move Gizmo while editing the Collider - just click the fold-out arrow on the Sprite Renderer component in the Inspector to collapse it.