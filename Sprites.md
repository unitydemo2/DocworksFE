#Sprites

__Sprites__ are 2D Graphic objects. If you are used to working in 3D, __Sprites__ are essentially just standard textures but there are special techniques for combining and managing sprite textures for efficiency and convenience during development.


Unity provides a placeholder [Sprite Creator](SpriteCreator),  a built-in [Sprite Editor](SpriteEditor), a [Sprite Renderer](class-SpriteRenderer) and a [Sprite Packer](SpritePacker)

See ***Importing and Setting up Sprites*** below for information on setting up assets as __Sprites__ in your Unity project.

##Sprite Tools

**Sprite Creator**

Use the [Sprite Creator](SpriteCreator) to create placeholder sprites in your project, so you can carry on with development without having to source or wait for graphics.

**Sprite Editor**

The [Sprite Editor](SpriteEditor) lets you extract sprite graphics from a larger image and edit a number of component images within a single texture in your image editor. You could use this, for example, to keep the arms, legs and body of a character as separate elements within one image.
 
**Sprite Renderer**

Sprites are rendered with a [Sprite Renderer](class-SpriteRenderer) component rather than the [Mesh Renderer](class-MeshRenderer) used with 3D objects. Use it to display images as __Sprites__ for use in both 2D and 3D scenes.

**Sprite Packer**

Use [Sprite Packer](SpritePacker) to opimize the use and performance of video memory by your project.

##Importing and Setting Up Sprites
__Sprites__ are a type of __Asset__ in  Unity projects. You can see them, ready to use, via the __Project View__. 

There are two ways to bring __Sprites__ into your project:

1. In your computer's Finder (Mac OS X)  or File Explorer (Windows), place your image directly into your Unity project's __Assets__ folder. 

    Unity detects this and displays it in your project's __Project View__.
    
2. In Unity, go to __Assets>Import New Asset...__ to bring up your computer's Finder (Mac OS X)  or File Explorer (Windows). 

    From there, select the image you want, and Unity puts it in the __Project View__.

See [Importing Assets](ImportingAssets) for more details on this and important information about organising your __Assets__ folder.

**Setting your  Image as a Sprite**

If your project mode is set to 2D, the image you import is automatically set as a __Sprite__. 

However, if your project mode is set to 3D, your image is set as a __Texture__, so you need to change the asset's __Texture Type__:

1. Click on the asset to see its __Import Inspector__. 
2. Set the __Texture Type__ to __Sprite (2D and UI)__.
    
    *(See Fig 1: Set Texture Type....)*

See [2D or 3D Projects](2Dor3D) for details on setting your project mode to 2D.


![Fig 1: Set Texture Type to Sprite (2D and UI) in the asset's inspector](../uploads/Main/TextureTypeSprite.png)



