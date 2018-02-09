Flare
=====


__Flare__ objects are the source assets that are used by [Lens Flare Components](class-LensFlare). The Flare itself is a combination of a texture file and specific information that determines how the Flare behaves. Then when you want to use the Flare in a __Scene__, you reference the specific Flare from inside a __LensFlare__ __Component__ attached to a __GameObject__.

There are some sample Flares in the [Standard Assets](HOWTO-InstallStandardAssets) package. If you want to add one of these to your scene, attach a [Lens Flare](class-LensFlare) Component to a GameObject, and drag the Flare you want to use into the __Flare__ property of the Lens Flare, just like assigning a __Material__ to a __Mesh Renderer__.


![The Flare Inspector](../uploads/Main/FlareInspector.png) 

Flares work by containing several Flare __Elements__ on a single __Texture__. Within the Flare, you pick and choose which __Elements__ you want to include from any of the Textures. 

Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Elements__ |The number of Flare images included in the Flare. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Image Index__ |Which Flare image to use from the __Flare Texture__ for this Element. See the _Flare Textures_ section below for more information. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Position__ |The Element's offset along a line running from the containing GameObject's position through the screen center. 0 = GameObject position, 1 = screen center. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Size__ |The size of the element. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Color__ |Color tint of the element. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Use Light Color__ |If the Flare is attached to a Light, enabling this will tint the Flare with the Light's color. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Rotate__ |If enabled, bottom of the Element will always face the center of the screen, making the Element spin as the Lens Flare moves around on the screen. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Zoom__ |If enabled, the Element will scale up when it becomes visible and scale down again when it isn't. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Fade__ |If enabled, the Element will fade in to full strength when it becomes visible and fade out when it isn't. |
|__Flare Texture__ |A texture containing images used by this Flare's __Elements__. It must be arranged according to one of the __TextureLayout__ options. |
|__Texture Layout__ |How the individual Flare Element images are laid out inside the __Flare Texture__ (see _Texture Layouts_ below for further details).|
|__Use Fog__ |If enabled, the Flare will fade away with distance fog. This is used commonly for small Flares. |


Details
-------


A Flare consists of multiple __Elements__, arranged along a line. The line is calculated by comparing the position of the GameObject containing the Lens Flare to the center of the screen. The line extends beyond the containing GameObject and the screen center. All Flare __Elements__ are strung out on this line.


Flare Textures
--------------


For performance reasons, all __Elements__ of one Flare must share the same Texture. This Texture contains a collection of the different images that are available as Elements in a single Flare. The __Texture Layout__ defines how the __Elements__ are laid out in the __Flare Texture__.


Texture Layouts
---------------


These are the options you have for different Flare __Texture Layouts__. The numbers in the images correspond to the __Image Index__ property for each __Element__.


###1 Large 4 Small

![](../uploads/Main/FlaresLayout0.png) 

Designed for large sun-style Flares where you need one of the __Elements__ to have a higher fidelity than the others. This is designed to be used with Textures that are twice as high as they are wide.

###1 Large 2 Medium 8 Small

![](../uploads/Main/FlaresLayout1.png) 

Designed for complex flares that require 1 high-definition, 2 medium and 8 small images. This is used in the standard assets "50mm Zoom Flare" where the two medium Elements are the rainbow-colored circles. This is designed to be used with textures that are twice as high as they are wide.
###1 Texture

![](../uploads/Main/FlaresLayout2.png) 

A single image.

2x2 grid
--------


![](../uploads/Main/FlaresLayout3.png) 

A simple 2x2 grid.

###3x3 grid

![](../uploads/Main/FlaresLayout4.png) 

A simple 3x3 grid.

###4x4 grid

![](../uploads/Main/FlaresLayout5.png) 

A simple 4x4 grid.

Hints
-----


* If you use many different Flares, using a single __Flare Texture__ that contains all the __Elements__ will give you best rendering performance.
* Lens Flares are blocked by __Colliders__. A Collider in-between the Flare GameObject and the Camera will hide the Flare, even if the Collider does not have a __Mesh Renderer__. If the in-between Collider is marked as Trigger it will block the flare if and only if __Physics.queriesHitTriggers__ is true.
* To override the shader used for Flares copy the Internal-Flare.shader shader from the [Built-in shaders](http://unity3d.com/support/resources/assets/built-in-shaders) into a folder named "Resources" in your "Assets" folder.
