#Sprite Editor


Sometimes a sprite texture contains just a single graphic element but it is often more convenient to combine several related graphics together into a single image. For example, the image could contain component parts of a single character, as with a car whose wheels move independently of the body. Unity makes it easy to extract elements from a composite image by providing a __Sprite Editor__ for the purpose.

**NOTE:**

Make sure the graphic you want to edit has its __Texture Type__ set to __Sprite (2D and UI)__. For information on importing and setting up sprites, see [Sprites](Sprites).

Sprite textures with multiple elements need the __Sprite Mode__ to be set to __Multiple__ in the Inpsector. (See *Fig 2: Texture Import Inspector...*  below.)


##Opening the Sprite Editor

To open the __Sprite Editor__:

1. Select the 2D image you want to edit from the __Project View__ *(Fig 1: Project View)*. 
    
    Note that you can't edit a sprite which is in the __Scene View__.

2. Click on the __Sprite Editor__ button in the  __Texture Import Inspector__ *(Fig 2: Texture Import Inspector)* and the __Sprite Editor__ displays *(Fig 3: Sprite Editor)*.

**Note:** You can only see the __Sprite Editor__ button if the __Texture Type__ on the image you have selected is set to __Sprite (2D and UI)__.



![Fig 1: Project View](../uploads/ProjectViewSprite.png)

![Fig 2: Texture Import Inspector with Sprite Editor button](../uploads/SpriteEditorButton.png)

**Note:** Set the  __Sprite Mode__ to __Multiple__ in the __Texture Import Inspector__ if your image has several elements.


![Fig 3: Sprite Editor](../uploads/SpriteEditor.png)



Along with the composite image, you will see a number of controls in the bar at the top of the window. The slider at the top right controls the zoom, while the color bar button to its left chooses whether you view the image itself or its alpha levels. The right-most slider controls the pixelation (mipmap) of the texure.  Moving the slider to the left reduces the resolution of the sprite texture. The most important control is the __Slice__ menu at the top left, which gives you options for separating the elements of the image automatically. Finally, the __Apply__ and __Revert__ buttons allow you to keep or discard any changes you have made.


##Using the Editor


The most direct way to use the editor is to identify the elements manually. If you click on the image, you will see a rectangular selection area appear with handles in the corners. You can drag the handles or the edges of the rectangle to resize it around a specific element. Having isolated an element, you can add another by dragging a new rectangle in a separate part of the image. You'll notice that when you have a rectangle selected, a panel appears in the bottom right of the window:

![](../uploads/Main/SpritePanel.png)

The controls in the panel let you choose a name for the sprite graphic and set the position and size of the rectangle by its coordinates.  A border width, for left, top, right and bottom can be specified in pixels. There are also settings for the sprite's pivot, which Unity uses as the coordinate origin and main "anchor point" of the graphic. You can choose from a number of default rectangle-relative positions (eg, Center, Top Right, etc) or use custom coordinates.

The __Trim__ button next to the Slice menu item will resize the rectangle so that it fits tightly around the edge of the graphic based on transparency.

**Note:** Borders are only supported for the UI system, not for the 2D SpriteRenderer.

##Automatic Slicing


Isolating the sprite rectangles manually works well but in many cases, Unity can save you work by detecting the graphic elements and extracting them for you automatically. If you click on the __Slice__ menu in the control bar, you will see this panel:

![](../uploads/Main/SpriteSlicePanelAuto.png)

With the slicing type set to __Automatic__, the editor will attempt to guess the boundaries of sprite elements by transparency. You can  set a default pivot for each identified sprite. The __Method__ menu lets you choose how to deal with existing selections in the window. The __Delete existing__ option will simply replace whatever is already selected, __Smart__ will attempt to create new rectangles while retaining or adjusting existing ones, and __Safe__ will add new rectangles without changing anything already in place.

__Grid by Cell Size__ or __Grid by Cell Count__ options are also available for the slicing type. This is very useful when the sprites have already been laid out in a regular pattern during creation:

![](../uploads/Main/SpriteSlicePanelGrid.png)

The __Pixel Size__ values determine the height and width of the tiles in pixels. If you chose grid by cell count, __Column & Row__ determines the number of columns and rows used for slicing. You can also use the __Offset__ values to shift the grid position from the top-left of the image and the __Padding__ values to inset the sprite rectangles slightly from the grid. The __Pivot__ can be set with one of nine preset locations or a __Custom Pivot__ location can be set.

Note that after any of the automatic slicing methods has been used, the generated rectangles can still be edited manually. You can let Unity handle the rough definition of the sprite boundaries and pivots and then do any necessary fine tuning yourself.

##Polygon Resizing
Open the __Sprite Editor__ for a polygon and you have the option to change its shape, size, and pivot position.


**Shape** 

![Sprite Editor: Polygon resizing - shape](../uploads/Main/SpriteEditorWindow.png)

Enter the number of sides you want the polygon to have in the __Sides__ field and click __Change__.

**Size and Pivot**

![Sprite Editor: Polygon resizing - size and pivot point - click on the polygon to display these options](../uploads/Main/SpriteEditorWindow2.png)

SIZE: To change the polygon's size, click on the sprite to display green border lines and the Sprite information box. Click and drag on the green lines to create the border you want, and the values in the __Border__ fields change. 
(Note that you cannot edit the __Border__ fields directly.)

PIVOT: To change the polygon's pivot point (that is the axis point the polygon moves around), click on the image to display the Sprite information box. Click on the __Pivot__ drop down menu and select an option. This displays a blue pivot circle on the polygon; its location depends on the pivot option to you have selected.  If you want to change it further, select __Custom Pivot__ and click and drag on the blue pivot circle to position it. 
(Note that you cannot edit the __Pivot__ fields directly.)






