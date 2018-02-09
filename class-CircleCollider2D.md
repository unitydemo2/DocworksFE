Circle Collider 2D
==================
The __Circle Collider 2D__ class is a collider for use with 2D physics. The collider's shape is a circle with a defined position and radius in the local coordinate space of a __Sprite__.


![](../uploads/Main/CircleCollider2DInspector.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Density__ |Changing the density here affects the mass of the GameObject's associated Rigidbody 2D. If you set the value to zero, its associated Rigidbody 2D ignores the Circle Collider 2D for all mass calculations, including centre of mass calculations. Note that this option is only available if you have selected __Use Auto Mass__ in an associated Rigidbody 2D.  |
|__Material__ |A physics material that determines properties of collisions, such as friction and bounce. |
|__Is Trigger__ |Check this if you want the Circle Collider 2D to behave as a trigger. |
|__Used by Effector__ |Check this if you want the Circle Collider 2D to be used by an attached Effector 2D. |
|__Offset__ |The local offset of the Circle Collider 2D geometry. |
|__Radius__ |Radius of the circle in local space units. |