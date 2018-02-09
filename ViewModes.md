#Scene view Control Bar

The Scene view control bar lets you choose various options for viewing the Scene and also control whether lighting and audio are enabled. These controls only affect the Scene view during development and have no effect on the built game.

![](../uploads/Main/SceneViewControlBar.png)

##Draw mode

The first drop-down menu selects which __Draw Mode__ will be used to depict the Scene. The available options are:

###Shading mode
* __Shaded__: show surfaces with their textures visible.
* __Wireframe__: draw meshes with a wireframe representation.
* __Shaded Wireframe__: show meshes textured and with wireframes overlaid.


###Miscellaneous
* __Shadow Cascades__: show directional light [shadow cascades](DirLightShadows).
* __Render Paths__: show the [rendering path](RenderingPaths) for each object using a color code: Blue indicates [deferred shading](RenderTech-DeferredShading), Green indicates [deferred lighting](RenderTech-DeferredLighting), yellow indicates [forward rendering](RenderTech-ForwardRendering) and red indicates [vertex lit](RenderTech-VertexLit).
* __Alpha Channel__: render colors with alpha.
* __Overdraw__: render objects as transparent "silhouettes". The transparent colors accumulate, making it easy to spot places where one object is drawn over another.
* __Mipmaps__: show ideal texture sizes using a color code: red indicates that the texture is larger than necessary (at the current distance and resolution); blue indicates that the texture could be larger. Naturally, ideal texture sizes depend on the resolution at which the game will run and how close the camera can get to particular surfaces.


###Deferred

These modes let you view each of the elements of the G-buffer (__Albedo__, __Specular__, __Smoothness__ and __Normal__) in isolation. See documentation on [Deferred Shading](RenderTech-DeferredShading) for more information.

###Global Illumination

The following modes are available to help visualise aspects of the [Global Illumination](GlobalIllumination) system: __UV Charts__, __Systems__, __Albedo__, __Emissive__, __Irradiance__, __Directionality__, __Baked__, __Clustering__ and __Lit Clustering__. See documentation on [GI Visualisations](GIVis) for informaiton about each of these modes.

##2D, lighting and Audio switches

To the right of the __Render Mode__ menu are three buttons that switch certain Scene view options on or off:

* __2D__: switches between 2D and 3D view for the Scene. In 2D mode the camera is oriented looking towards positive z, with the x axis pointing right and the y axis pointing up.
* __Lighting__: turns Scene view lighting (lights, object shading, etc) on or off.
* __Audio__: turns Scene view audio effects on or off.

##Effects button and menu

The menu (activated by the small mountain icon to the right of the __Audio__ button) has options to enable or disable rendering effects in the Scene view.

* __Skybox__: a skybox texture rendered in the Scene's background
* __Fog__: gradual fading of the view to a flat color with distance from the camera.
* __Flares__: lens flares on lights.
* __Animated Materials__: should animated materials show the animation?

The __Effects__ button itself acts as a switch that enables or disables all the effects at once.

##Gizmos menu

The Gizmos menu contains lots of options for how objects, icons, and gizmos are displayed. This menu is available in both the Scene view and the [Game view](GameView). See documentation on the [Gizmos Menu](GizmosMenu) manual page for more information.

##Search box

The rightmost item on the control bar is a search box that lets you filter items in the Scene view by their names and/or types (you can select which with the small menu at the left of the search box). The set of items that match the search filter are also be shown in the Hierarchy view which, by default, is located to the left of the Scene view.