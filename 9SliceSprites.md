# 9-slicing Sprites 

9-slicing is a 2D technique which allows you to reuse an image at various sizes without needing to prepare multiple [Assets](AssetWorkflow). It involves splitting the image into nine portions, so that when you re-size the [Sprite](Sprites), the different portions scale or tile (that is, repeat in a grid formation) in different ways to keep the Sprite in proportion. This is useful when creating patterns or [Textures](class-TextureImporter), such as walls or floors in a 2D environment.

This is an example of a 9-sliced Sprite, split into nine sections. Each section is labelled with a letter from A to I.

![](../uploads/Main/9SliceSprites-0.png)

The following points describe what happens when you change the dimensions of the image:

* The four corners (A, C, G and I) do not change in size.

* The B and H sections stretch or tile horizontally.

* The D and F sections stretch or tile vertically.

* The E section stretches or tiles both horizontally and vertically.

This page describes how to set 9-slicing up, and which settings to apply depending on whether you want to stretch or tile the areas shown above.

## Setting up your Sprite for 9-slicing

Before you 9-slice a Sprite, you need to ensure the Sprite is set up properly.

First, you need to make sure the __Mesh Type__ is set to __Full Rect__. To apply this, select the Sprite, then in the Inspector window click the __Mesh Type__ drop-down and select __Full Rect__. If the __Mesh Type__ is set to __Tight__, 9-slicing might not work correctly, because of how the Sprite Renderer generates and renders the Sprite when it is set up for 9-slicing. 

![The Sprite’s Inspector window. __Mesh Type__ is highlighted in the red box.](../uploads/Main/9SliceSprites-1.png)

Next, you need to define the borders of the Sprite via the [__Sprite Editor__](SpriteEditor) window. To do this, select the Sprite, then in the [Inspector](UsingTheInspector) window click the __Sprite Editor__ button.

![The Sprite’s Inspector window. The __Sprite Editor__ button is highlighted in the red box. See documentation on [Sprites](Sprites) for information on all of the properties in the Sprite Import Settings.](../uploads/Main/9SliceSprites-2.png)

Use the Sprite Editor window to define the borders of the Sprite (that is, where you want to define the tiled areas, such as the walls of a floor tile). To do this, use the Sprite control panel’s __L__, __R__, __T__, and __B__ fields (left, right, top, and bottom, respectively). Alternatively, click and drag the green dots at the top, bottom, and sides.

![Defining the borders of the Sprite in the Sprite Editor window](../uploads/Main/9SliceSprites-3.png)

Click __Apply__ in the Sprite Editor window’s top bar. Close the Sprite Editor window, and drag the Sprite from the [Project window](ProjectView) into the Scene view to begin working on it.

## 9-slicing your Sprite

Select the Sprite in the [Scene view](UsingTheSceneView) or the [Hierarchy window](Hierarchy). In the Inspector window, navigate to the [Sprite Renderer](class-SpriteRenderer) component and change the __Draw Mode__ property. 

![](../uploads/Main/SpriteRenderer.png)

It is set to __Simple__ by default; to apply 9-slicing, set it to either __Sliced__ or __Tiled__ depending on the behavior you want. The follow sections explain how each one behaves, using this Sprite:

![The original Sprite used for the examples shown below](../uploads/Main/9SliceSprites-4.png)

### Simple

![](../uploads/Main/9SliceSprites-5.png)

This is the default Sprite Renderer behaviour. The image scales in all directions when its dimensions change. __Simple__ is not used for 9-slicing.

### Sliced

![](../uploads/Main/9SliceSprites-6.png)

In __Sliced__ mode, the corners stay the same size, the top and bottom of the Sprite stretch horizontally, the sides of the Sprite stretch vertically, and the centre of the Sprite stretches horizontally and vertically to fit the Sprite’s size.

When a Sprite’s __Draw Mode__ is set to __Sliced__, you can choose to change the size using the __Size__ property on the Sprite Renderer or the [Rect Transform Tool](Toolbar). You can still scale the Sprite using the Transform properties or the Transform Tool; however, the Transform scales the Sprite without applying the 9-slicing. 

### Tiled

![](../uploads/Main/9SliceSprites-7.png)

In __Tiled__ mode, the sprite stays the same size, and does not scale. Instead, the top and bottom of the Sprite repeat horizontally, the sides repeat vertically, and the centre of the Sprite repeats in a tile formation to fit the Sprite’s size.

When a Sprite’s __Draw Mode__ is set to __Sliced__, you can choose to change the size using the __Size__ property on the Sprite Renderer or the [Rect Transform Tool](Toolbar). You can still scale the Sprite using the Transform properties or the Transform Tool; however, the Transform scales the Sprite without applying the 9-slicing. 

When you set the __Draw Mode__ to __Tiled__, an additional property called __Tile Mode__ appears. See the next section in this page for more information on how __Tile Mode__ works. 

See documentation on the [Sprite Renderer](class-SpriteRenderer) for full details on all of the component’s properties.

## Tile Mode

When the __Draw Mode__ is set to __Tiled__, use the __Tile Mode__ property to control how the sections repeat when the dimensions of the Sprite change.

### ![Set __Draw Mode__  to  __Tiled__  to access __Tile Mode__ in  __Sprite Renderer__](../uploads/Main/9SliceSprites-8.png)

### Continuous

__Tile Mode__ is set to __Continuous__ by default. When the size of the Sprite changes, the repeating sections repeat evenly in the Sprite.

![](../uploads/Main/9SliceSprites-9.png)

### Adaptive

When __Tile Mode__ is set to __Adaptive__, the repeating sections only repeat when the dimensions of the Sprite reach the __Stretch Value__. 

![](../uploads/Main/9SliceSprites-10.png)

Use the __Stretch Value__ slider to set the value between __0__ and __1__. Note that __1__ represents an image resized to twice its original dimensions, so if the __Stretch Value__ is set at __1__, the section repeats when the image is stretched to twice its original size.

To demonstrate this, the following images show the difference between an image with the same dimension but a different __Stretch Value:__

__Stretch Value 0.1__:

![](../uploads/Main/9SliceSprites-11.png)

__Stretch Value 0.5__:

![](../uploads/Main/9SliceSprites-12.png)

## 9-slicing and Colliders

If your [Sprite](Sprites) has a [Collider2D](Collider2D) attached, you need to ensure that when you change the Sprite’s dimensions, the Collider2D changes with it.

[Box Collider 2D](class-BoxCollider2D) and [Polygon Collider 2D](class-PolygonCollider2D) are the only Collider2D components in Unity that support 9-slicing. These two Collider2Ds have an __Auto Tiling__ checkbox. To make sure the Collider2D components are set up for 9-slicing, select the Sprite you are applying it to, navigate to the Collider2D in the Inspector window, and tick the __Auto Tiling__ checkbox. This enables automatic updates to the shape of the Collider2D, meaning that the shape is automatically readjusted when the Sprite’s dimensions change. If you don’t enable __Auto Tiling__, the Collider2D stays the same shape and size, even when the Sprite’s dimensions change.

### Limitations and known issues

* The only two Collider2Ds that support 9-slicing are BoxCollider2D and PolygonCollider2D.

* You cannot edit BoxCollider2D or PolygonCollider2D when the Sprite Renderer’s __Draw Mode__ is set to __Sliced__ or __Tiled__. Editing in the Inspector window is disabled, and a warning appears to notify you that the Collider2D cannot be edited because it is driven by the Sprite Renderer component’s tiling properties.

* When the shape is regenerated in __Auto Tiling__, additional edges might appear within the Collider2D’s shape. This may have an effect on collisions.

