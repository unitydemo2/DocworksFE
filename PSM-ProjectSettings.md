Unity for PSM Project Settings
===

Unity for PSM comes with additional project (build and player) settings.

Build Settings: General

* Build Type

Player Settings:

* Icon
* Splash Image
* Other Settings


----

## Build Settings
### Build Type
**DevAssistant**

* Creates a development package to be launched from the Development Assistant
* Option to use development player ( for player connection, profiler and script debugging)
* Autoconnect Profiler option
* Enable script debugging option
* See [Creating and Running Unity for PSM Apps](PSMBuildingampRunning) for further information.

**Master**

* Creates a master package for submission to the PlayStation&#174;Store.
* This option clears the development build settings, since these are not available in a master build.
* See [Creating a Master Package](PSMMasterPackage) for further information.

**Intermediate**

* Creates a _raw_ output folder - before the master packaging is started.
* This option is useful when the Developer and Publisher are separate entities.
* It enables the Developer to defer the master package creation step to the Publisher.
* See [Creating a Master Package](PSMMasterPackage) for further information.

## Player Settings
## Icon
The Icon (Override for PSM) option should be ticked in order to add a Still Image icon.

_Image Format_

* 128x128, 256x256 and 512x512 pixels in size
* PNG

![Figure 1. Icon Settings for PSM](../uploads/Main/psm_icon_setting.png) 

## Splash Image
The Splash Image or Start-up Image will immediately display when the game is launched.

_Image Format_

* 854x480 pixels in size
* 8-bit PNG (the image is converted, but for best image quality use a matching bit depth)

## Other Settings
**Rendering**

_Static Batching_

* Static batching allows the engine to reduce draw calls for geometry of any size (provided it does not move and shares the same material). 
Static batching is significantly more efficient than dynamic batching. 
You should choose static batching as it will require less CPU power. 
(Activated by default).

_Dynamic Batching_

* Unity can automatically batch moving objects into the same draw call if they share the same material and fulfill other criteria.  
Dynamic batching is done automatically and does not require any additional effort on your side.

The benefits of static and dynamic batching can vary greatly from game to game. For general information and tips on using Static and Dynamic batching, please see [DrawCallBatching](DrawCallBatching)

_GPU Skinning_

* Uses DX11/ES3 type GPU Skinning to greatly increase the rendering speed of skinned meshes.


