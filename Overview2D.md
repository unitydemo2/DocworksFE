#Gameplay in 2D

While famous for its 3D capabilities, Unity can also be used to create 2D games. The familiar functions of the editor are still available but with helpful additions to simplify 2D development.

![Scene viewed in 2D mode](../uploads/Main/Overview2D.png)

The most immediately noticeable feature is the _2D_ view mode button in the toolbar of the Scene view. When 2D mode is enabled, an orthographic (ie, perspective-free) view will be set; the camera looks along the Z axis with the Y axis increasing upwards. This allows you to visualise the scene and place 2D objects easily.

For a full list of 2D components, how to switch between 2D and 3D mode, and the different 2D and 3D Mode settings, see [2D or 3D Projects](2Dor3D).



##2D Graphics

Graphic objects in 2D are known as __Sprites__. Sprites are essentially just standard textures but there are special techniques for combining and managing sprite textures for efficiency and convenience during development. Unity provides a built-in [Sprite Editor](SpriteEditor) to let you extract sprite graphics from a larger image. This allows you to edit a number of component images within a single texture in your image editor. You could use this, for example, to keep the arms, legs and body of a character as separate elements within one image.

Sprites are rendered with a [Sprite Renderer](class-SpriteRenderer) component rather than the [Mesh Renderer](class-MeshRenderer) used with 3D objects. You can add this to a GameObject via the Components menu (__Component > Rendering > Sprite Renderer__ or alternatively, you can just create a GameObject directly with a Sprite Renderer already attached (menu: __GameObject &gt; 2D Object &gt; Sprite__).

In addition, you can use a [Sprite Creator](SpriteCreator) tool to make placeholder 2D images.


##2D Physics

Unity has a separate physics engine for handling 2D physics so as to make use of optimizations only available with 2D. The components correspond to the standard 3D physics components such as [Rigidbody](class-Rigidbody), [Box Collider](class-BoxCollider) and [Hinge Joint](class-HingeJoint), but with "2D" appended to the name. So, sprites can be equipped with [Rigidbody 2D](class-Rigidbody2D), [Box Collider 2D](class-BoxCollider2D) and [Hinge Joint 2D](class-HingeJoint2D). Most 2D physics components are simply "flattened" versions of the 3D equivalents (eg, _Box Collider 2D_ is a square while _Box Collider_ is a cube) but there are a few exceptions.

For a full list of 2D Physics components, see [2D or 3D Projects](2Dor3D).  See the [Physics](PhysicsSection) section of the manual for further information about 2D physics concepts and components.