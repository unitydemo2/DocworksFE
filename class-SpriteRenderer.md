Sprite Renderer
---------------

The __Sprite Renderer__ component lets you display images as __Sprites__ for use in both 2D and 3D scenes.

Add it to a GameObject via the Components menu (__Component > Rendering > Sprite Renderer__ or alternatively, you can just create a GameObject directly with a Sprite Renderer already attached (menu: __GameObject &gt; 2D Object &gt; Sprite__).

![](../uploads/Main/SpriteRenderInspector.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Sprite__ |The Sprite object to render. Sprite objects can  be generated from textures by using the Sprite setting on the [Texture importer](class-TextureImporter). |
|__Color__ |Vertex color of the rendered mesh. |
|__Flip__ |Flip the sprite in the X or Y planes. |
|__Material__ |Material used to render the sprite. |
| __Draw Mode__ | Select an option from the Draw Mode drop-down box to define how the Sprite scales when you change its dimensions.  |
|&nbsp;&nbsp;&nbsp;&nbsp;Simple| This is the default Sprite Renderer behavior. The image scales in all directions when its dimensions change. |
|&nbsp;&nbsp;&nbsp;&nbsp;Sliced| Use Sliced if you intend to apply 9-slicing to an image, and you want the sections to stretch. In Sliced mode, the corners stay the same size, the top and bottom of the Sprite stretch horizontally, the sides of the Sprite stretch vertically, and the centre of the Sprite stretches horizontally and vertically to fit the Sprite’s size. See documentation on [9-slicing Sprites](9SliceSprites) for more information. |
|&nbsp;&nbsp;&nbsp;&nbsp;Size| Use this to change the horizontal and vertical size of the Sprite. You must use this to change the size of the Sprite if you want the 9-slicing to work; the default Transform component only applies a default scale.  |
|&nbsp;&nbsp;&nbsp;&nbsp;Tiled| Use Tiled if you intend to apply 9-slicing to an image, and you want the sections to repeat. In Tiled mode, the sprite stay the same size, and does not scale. Instead, the top and bottom of the Sprite repeat horizontally, the sides repeat vertically, and the centre of the Sprite repeats in a tile formation to fit the Sprite’s size. See documentation on [9-slicing Sprites](9SliceSprites) for more information. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Size| Use this to change the horizontal and vertical size of the Sprite. You must use this to change the size of the Sprite if you want the 9-slicing to work; the default Transform component only applies a default scale.  |
|&nbsp;&nbsp;&nbsp;&nbsp;Tile Mode| When the Draw Mode is set to Tiled, use the Tile Mode property to control how the sections repeat when the dimensions of the Sprite change. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Continuous| Tile Mode is set to Continuous by default. When the size of the Sprite changes, the repeating sections repeat evenly in the Sprite. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Adaptive| When Tile Mode is set to Adaptive, the repeating sections only repeat when the dimensions of the Sprite reach the Stretch Value.   |
|&nbsp;&nbsp;&nbsp;&nbsp;Stretch Value| Use the Stretch Value slider to set the value between 0 and 1. Note that 1 represents an image resized to twice its original dimensions, so if the Stretch Value is set at 1, the section repeats when the image is stretched to twice its original size. |
|__Sorting Layer__ |The [layer](Layers) used to define this sprite's overlay priority during rendering. |
|__Order In Layer__ |The overlay priority of this sprite within its layer. Lower numbers are rendered first and subsequent numbers overlay those below. |


##Details

In 3D graphics, an object's appearance will vary according to lighting and the position from which it is viewed. In 2D, by contrast, an image is simply displayed onscreen with no transformations other than basic position, scale and rotation. A sprite's position is given by a 2D coordinate, so there is no concept of "depth" or distance from camera when rendering.

However, it is still very important to have some way to determine the overlay priority of different sprites (ie, which sprites will obscure others when they cross paths). For example, in a driving game, a car should be seen to pass over flat objects on the road surface. Unity uses the concept of __sorting layers__ to allow you to divide sprites into groups for overlay priority. Sprites with a sorting layer lower in the order will be overlaid by those in a higher sorting layer.

Sometimes, two or more objects in the same sorting layer can overlap (eg, two player characters in a side scrolling game). The _order in layer_ property can be used to apply consistent priorities to sprites in the same layer. As with sorting layers, the rule is that lower numbers are rendered first and can be obscured by the higher numbers rendered later. See the [layer manager page](class-TagManager) for details of editing sorting layers. If sorting layers are not used, standard depth-based sorting can be used.



###Rendering

A Sprite Renderer uses the texture supplied in the _Sprite_ property but uses the shader and other properties from the _Material_ property (this is actually accomplished using a [MaterialPropertyBlock](ScriptRef:MaterialPropertyBlock.html) behind the scenes). This means that you can use the same material to render different sprites without worrying about which texture is assigned on the material.

The sprite is rendered on a mesh that uses position, color and UV at each vertex but no normal vector. If your material requires normal vectors then you can calculate them using a vertex shader (see the [Surface Shader Examples](SL-SurfaceShaderExamples) page for further details).

The default shaders used for sprites are:

* **Sprites/Default** - a simple alpha blended shader that does not interact with lights in the scene.

* **Sprites/Diffuse** - a simple alpha-blended surface shader that _does_ interact with  lights. This generates a front-facing normal vector (0,0,-1).


###Flipping

While Sprites can be flipped by setting negative ``transform.scale``, this has the side effect of also flipping the child GameObjects and also flipping the colliders, which can be performance intensive or otherwise not preferred.

The SpriteRenderer flipping feature provides a lightweight alternative which doesn’t affect any other components or GameObjects. It simply flips the rendered sprite on x or y axis and nothing else.
