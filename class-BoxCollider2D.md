Box Collider 2D
===============

The __Box Collider 2D__ component is a Collider for use with 2D physics. Its shape is a rectangle with a defined position, width and height in the local coordinate space of a __Sprite__. Note that the rectangle is axis-aligned - that is, its edges are parallel to the X or Y axes of local space.

![](../uploads/Main/BoxCollider2DInspector.png) 

|**_Property_** |**_Function_** |
|:---|:---|
|__Material__ |A physics Material that determines properties of collisions, such as friction and bounce. |
|__Is Trigger__ |Check this box if you want the Box Collider 2D to behave as a trigger. |
|__Used by Effector__ |Check this box if you want the Box Collider 2D to be used by an attached Effector 2D component. |
| __Used by Composite__ | Tick this checkbox if you want this Collider to be used by an attached [Composite Collider 2D](class-CompositeCollider2D). <br/><br/>When you enable __Used by Composite__, other properties disappear from the Box Collider 2D component, because they are now controlled by the attached Composite Collider 2D. The properties that disappear from the Box Collider 2D are __Material__, __Is Trigger__, __Used By Effector__, and __Edge Radius__. |
|__Auto Tiling__ |Tick this checkbox if the [Sprite Renderer](class-SpriteRenderer) component for the selected Sprite has the __Draw Mode__ set to __Tiled__. This enables automatic updates to the shape of the [Collider 2D](Collider2D), meaning that the shape is automatically readjusted when the Sprite’s dimensions change. If you don’t enable __Auto Tiling__, the Collider 2D geometry doesn’t automatically repeat. |
|__Offset__ |Set the local offset of the Collider 2D geometry. |
|__Size__ |Set the size of the box in local space units. |
| __Edge Radius__| Controls a radius around edges, so that vertices are circular. This results in a larger [Collider 2D](Collider2D) with rounded convex corners. The default value for this setting is __0__ (no radius). |

