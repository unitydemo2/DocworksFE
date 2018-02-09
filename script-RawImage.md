#Raw Image

The __Raw Image__ control displays a non-interactive image to the user. This can be used for decoration, icons, etc, and the image can also be changed from a script to reflect changes in other controls. The control is similar to the [Image](script-Image) control but does not have the same set of options for animating the image and accurately filing the control rectangle. However, the Raw Image can display any texture whilst the Image can only show a [Sprite](class-TextureImporter) texture.

![A Raw Image control](../uploads/Main/RawImageCtrlExample.png)

##Properties

![](../uploads/Main/UI_RawImageInspector.png)

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Texture__ |The texture that represents the image to display.|
|__Color__ |The color to apply to the image. |
|__Material__ | The [Material](class-Material) to use for rendering the image. |
|__UV Rectangle__ |The image's offset and size within the control rectangle, given in normalized coordinates (range 0.0 to 1.0). The edges of the image are stretched to fill the space around the UV rectangle. |


##Details

Since the Raw Image does not require a sprite texture, you can use it to display any texture available to the Unity player. For example, you might show an image downloaded from a URL using the [WWW](ScriptRef:WWW.html) class or a texture from an object in a game.

The _UV Rectangle_ properties allow you to display a small section of a larger image. The _X_ and _Y_ coordinates specify which part of the image is aligned with the bottom left corner of the control. For example, an X coordinate of 0.25 will cut off the leftmost quarter of the image. The _W_ and _H_ (ie, width and height) properties indicate the width and height of the section of image that will be scaled to fit the control rectangle. For example, a width and height of 0.5 will scale a quarter of the image area up to the control rectangle. By changing these properties, you can zoom and scale the image as desired (see also the [Scrollbar](script-Scrollbar) control).