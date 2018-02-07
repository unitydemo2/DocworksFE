#Quality Settings

Unity allows you to set the level of graphical quality it will attempt to render. Generally speaking, quality comes at the expense of framerate and so it may be best not to aim for the highest quality on mobile devices or older hardware since it will have a detrimental effect on gameplay. The __Quality Settings__ inspector (menu: __Edit &gt; Project Settings &gt; Quality__) is used to select the quality level in the editor for the chosen device. It is split into two main areas - at the top, there is the following matrix:


![](../uploads/Main/QualSettingsTop.png) 

Unity lets you assign a name to a given combination of quality options for easy reference. The rows of the matrix let you choose which of the different platforms each quality level will apply to. The Default row at the bottom of the matrix is not a quality level in itself but rather sets the default quality level used for each platform (a green checkbox in a column denotes the level currently chosen for that platform). Unity comes with six quality levels pre-enabled but you can add your own levels using the button below the matrix. You can use the trashcan icon (the rightmost column) to delete an unwanted quality level.

You can click on the name of a quality level to select it for editing, which is done in the panel below the settings matrix:


![](../uploads/Main/QualitySettingsBottom.png) 


The quality options you can choose for a quality level are as follows:

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Name__|The name that will be used to refer to this quality level|

## Rendering

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Pixel Light Count__|The maximum number of pixel lights when Forward Rendering is used.|
|__Texture Quality__|This lets you choose whether to display textures at maximum resolution or at a fraction of this (lower resolution has less processing overhead). The options are **Full Res**, **Half Res**, **Quarter Res** and **Eighth Res**.|
|__Anisotropic Textures__|This enables if and how anisotropic textures will be used. The options are __Disabled__, __Per Texture__ and __Forced On__ (ie, always enabled). |
|__AntiAliasing__|This sets the level of antialiasing that will be used. The options are **2x**, **4x** and **8x** multi-sampling.|
|__Soft Particles__|Should soft blending be used for particles?|
|__Realtime Reflection Probes__|Should [reflection probes](class-ReflectionProbe) be updated during gameplay?|

## Shadows

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Shadows__|This determines which type of shadows should be used. The available options are __Hard and Soft Shadows__, __Hard Shadows Only__ and __Disable Shadows__. |
|__Shadow resolution__|Shadows can be rendered at several different resolutions: **Low**, **Medium**, **High** and **Very High**. The higher the resolution, the greater the processing overhead.|
|__Shadow Projection__|There are two different methods for projecting shadows from a directional light. **Close Fit** renders higher resolution shadows but they can sometimes wobble slightly if the camera moves. **Stable Fit** renders lower resolution shadows but they don't wobble with camera movements.|
|__Shadow Cascades__|The number of shadow cascades can be set to zero, two or four. A higher number of cascades gives better quality but at the expense of processing overhead (see [Directional Light Shadows](DirLightShadows) for further details).|
|__Shadow Distance__|The maximum distance from camera at which shadows will be visible. Shadows that fall beyond this distance will not be rendered.|
| __Shadowmask Mode__ | Sets the shadowmask behaviour when using the [Shadowmask](LightMode-Mixed-ShadowmaskMode) Mixed lighting mode. Use the Lighting window (menu: __Window__ > __Lighting__ > __Settings__) to set this up in your Scene. |
| &nbsp;&nbsp;&nbsp;&nbsp;Distance Shadowmask | Unity uses real-time shadows up to the __Shadow Distance__, and baked shadows beyond it. |
| &nbsp;&nbsp;&nbsp;&nbsp;Shadowmask | hadowmask: Static GameObjects that cast shadows always cast baked shadows. |
|__Shadow Near Plane Offset__|Offset shadow near plane to account for large triangles being distorted by shadow pancaking.|

## Other

|**_Property_:** |**_Function:_** |
|:---|:---|
|__Blend Weights__|The number of bones that can affect a given vertex during an animation. The available options are one, two or four bones.|
|__VSync Count__|Rendering can be synchronised with the refresh rate of the display device to avoid "tearing" artifacts (see below). You can choose to synchronise with every vertical blank (VBlank), every second vertical blank or not to synchronise at all.|
|__LOD Bias__|LOD levels are chosen based on the onscreen size of an object. When the size is between two LOD levels, the choice can be biased toward the less detailed or more detailed of the two models available. This is set as a fraction from 0 to +infinity.  When it is set between 0 and 1 it favors less detail.  A setting of more than 1 favors greater detail. For example, setting LOD Bias to 2 and having it change at 50% distance, LOD actually only changes on 25%. |
|__Maximum LOD Level__|The highest LOD that will be used by the game. See note below for more Information.|
|__Particle Raycast Budget__|The maximum number of raycasts to use for approximate particle system collisions (those with __Medium__ or __Low__ quality). See [Particle System Collision Module](class-ParticleSystem).|
|__Async Upload Time Slice__|The amount of CPU time in milliseconds per frame to spend uploading buffered textures to the GPU. See [Async Texture Upload](AsyncTextureUpload).|
|__Async Upload Buffer Size__|The size in MB for the Async Upload buffer. See [Async Texture Upload](AsyncTextureUpload).|


## MaximumLOD level

Models which have a LOD below the MaximumLOD level will not be used and omitted from the build (which will save storage and memory space). Unity will use the smallest LOD value from all the MaximumLOD values linked with the quality settings for the target platform. If an LOD level is included then models from that LODGroup will be included in the build and always loaded at runtime for that LODGroup, regardless of the quality setting being used. As an example, if LOD level 0 is used in any quality setting then all the LOD levels will be included in the build and all the referenced models loaded at runtime. 

## Tearing

The picture on the display device is not continuously updated but rather the updates happen at regular intervals much like frame updates in Unity. However, Unity's updates are not necessarily synchronised with those of the display, so it is possible for Unity to issue a new frame while the display is still rendering the previous one. This will result in a visual artifact called "tearing" at the position onscreen where the frame change occurs.


![Simulated example of tearing. The shift in the picture is clearly visible in the magnified portion.](../uploads/Main/Tearing.png) 

It is possible to set Unity to switch frames only during the period where the display device is not updating, the so-called "vertical blank". The VSync option on the Quality Settings synchronises frame switches with the device's vertical blank or optionally with every other vertical blank. The latter may be useful if the game requires more than one device update to complete the rendering of a frame.


### Anti-aliasing

Anti aliasing improves the appearance of polygon edges, so they are not "jagged", but smoothed out on the screen. However, it incurs a performance cost for the graphics card and uses more video memory (there's no cost on the CPU though). The level of anti-aliasing determines how smooth polygon edges are (and how much video memory does it consume).


![Without anti-aliasing, polygon edges are "jagged".](../uploads/Main/AntiAliasingNone.png) 


![With 4x anti-aliasing, polygon edges are smoothed out.](../uploads/Main/AntiAliasing4x.png) 

However, built-in hardware anti-aliasing does not work with [Deferred Shading](RenderTech-DeferredShading) or [HDR](HDR) rendering; for these cases you'll need to use [Antialiasing Image Effect](PostProcessing-Antialiasing).


### Soft Particles

Soft Particles fade out near intersections with other scene geometry. This looks much nicer, however it's more expensive to compute (more complex pixel shaders), and only works on platforms that support [depth textures](SL-DepthTextures). Furthermore, you have to use [Deferred Shading](RenderTech-DeferredShading) or [Legacy Deferred Lighting](RenderTech-DeferredLighting) rendering path, or make the camera render [depth textures](SL-CameraDepthTexture) from scripts.

![Without Soft Particles - visible intersections with the scene.](../uploads/Main/SoftParticlesOff.png) 

![With Soft Particles - intersections fade out smoothly.](../uploads/Main/SoftParticlesOn.png) 

---

* <span class="page-edit">2017-09-18  <!-- include IncludeTextAmendPageSomeEdit --></span>

* <span class="page-history">__Shadowmask Mode__ added in [2017.1](https://docs.unity3d.com/2017.1/Documentation/Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>

