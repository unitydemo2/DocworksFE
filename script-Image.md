#Image

The __Image__ control displays a non-interactive image to the user. This can be used for decoration, icons, etc, and the image can also be changed from a script to reflect changes in other controls. The control is similar to the [Raw Image](script-RawImage) control but offers more options for animating the image and accurately filing the control rectangle. However, the Image control requires its texture to be a [Sprite](class-TextureImporter), while the Raw Image can accept any texture.

![An Image control](../uploads/Main/ImageCtrlExample.png)

##Properties

![](../uploads/Main/UI_ImageInspector.png)

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Source Image__ | The texture that represents the image to display (which must be imported as a [Sprite](class-TextureImporter)). |
|__Color__ | The color to apply to the image. |
|__Material__ | The [Material](class-Material) to use for rendering the image. |
|__Raycast Target__ | Should this be considered a target for raycasting? |
|__Preserve Aspect__ | Ensure image remains existing dimension.  |
|__Set Native Size__ | Button to set the dimensions of the image box to the original pixel size of the texture. |


##Details

The image to display must be imported as a [Sprite](class-TextureImporter) to work with the Image control. 
