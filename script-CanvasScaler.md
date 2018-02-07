# Canvas Scaler

The Canvas Scaler component is used for controlling the overall scale and pixel density of UI elements in the Canvas. This scaling affects everything under the Canvas, including font sizes and image borders.

![](../uploads/Main/UI_CanvasScalerInspector.png)

##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__UI Scale Mode__ |Determines how UI elements in the Canvas are scaled. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Constant Pixel Size__ |Makes UI elements retain the same size in pixels regardless of screen size. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Scale With Screen Size__ |Makes UI elements bigger the bigger the screen is. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Constant Physical Size__ |Makes UI elements retain the same physical size regardless of screen size and resolution. |

Settings for Constant Pixel Size:

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Scale Factor__ |Scales all UI elements in the Canvas by this factor. |
|__Reference Pixels Per Unit__ |If a sprite has this 'Pixels Per Unit' setting, then one pixel in the sprite will cover one unit in the UI. |

Settings for Scale With Screen Size:

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Reference Resolution__ |The resolution the UI layout is designed for. If the screen resolution is larger, the UI will be scaled up, and if it's smaller, the UI will be scaled down. |
|__Screen Match Mode__ |A mode used to scale the canvas area if the aspect ratio of the current resolution doesn't fit the reference resolution. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Match Width or Height__ |Scale the canvas area with the width as reference, the height as reference, or something in between. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Expand__ |Expand the canvas area either horizontally or vertically, so the size of the canvas will never be smaller than the reference. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Shrink__ |Crop the canvas area either horizontally or vertically, so the size of the canvas will never be larger than the reference. |
|__Match__ |Determines if the scaling is using the width or height as reference, or a mix in between. |
|__Reference Pixels Per Unit__ |If a sprite has this 'Pixels Per Unit' setting, then one pixel in the sprite will cover one unit in the UI. |

Settings for Constant Physical Size:

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Physical Unit__ |The physical unit to specify positions and sizes in. |
|__Fallback Screen DPI__ |The DPI to assume if the screen DPI is not known. |
|__Default Sprite DPI__ |The pixels per inch to use for sprites that have a 'Pixels Per Unit' setting that matches the 'Reference Pixels Per Unit' setting. |
|__Reference Pixels Per Unit__ |If a sprite has this 'Pixels Per Unit' setting, then its DPI will match the 'Default Sprite DPI' setting. |

Settings for World Space Canvas (shown when Canvas component is set to World Space):

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Dynamic Pixels Per Unit__ |The amount of pixels per unit to use for dynamically created bitmaps in the UI, such as Text. |
|__Reference Pixels Per Unit__ |If a sprite has this 'Pixels Per Unit' setting, then one pixel in the sprite will cover one unit in the world. If the 'Reference Pixels Per Unit' is set to 1, then the 'Pixels Per Unit' setting in the sprite will be used as-is. |

##Details

For a Canvas set to 'Screen Space - Overlay' or 'Screen Space - Camera', the Canvas Scaler UI Scale Mode can be set to Constant Pixel Size, Scale With Screen Size, or Constant Physical Size.

### Constant Pixel Size
Using the Constant Pixel Size mode, positions and sizes of UI elements are specified in pixels on the screen. This is also the default functionality of the Canvas when no Canvas Scaler is attached. However, With the Scale Factor setting in the Canvas Scaler, a constant scaling can be applied to all UI elements in the Canvas.

### Scale With Screen Size
Using the Scale With Screen Size mode, positions and sizes can be specified according to the pixels of a specified reference resolution. If the current screen resolution is larger than the reference resolution, the Canvas will keep having only the resolution of the reference resolution, but will scale up in order to fit the screen. If the current screen resolution is smaller than the reference resolution, the Canvas will similarly be scaled down to fit.

If the current screen resolution has a different aspect ratio than the reference resolution, scaling each axis individually to fit the screen would result in non-uniform scaling, which is generally undesirable. Instead of this, the ReferenceResolution component will make the Canvas resolution deviate from the reference resolution in order to respect the aspect ratio of the screen. It is possible to control how this deviation should behave using the Screen Match Mode setting.

### Constant Physical Size
Using the Constant Physical Size mode, positions and sizes of UI elements are specified in physical units, such as millimeters, points, or picas. This mode relies on the device reporting its screen DPI correctly. You can specify a fallback DPI to use for devices that do not report a DPI.

### World Space
For a Canvas set to 'World Space' the Canvas Scaler can be used to control the pixel density of UI elements in the Canvas.

##Hints
* See the page [Designing UI for Multiple Resolutions](HOWTO-UIMultiResolution) for a step by step explanation of how Rect Transform anchoring and Canvas Scaler can be used in conjunction to make UI layouts that adapt to different resolutions and aspect ratios.