Skybox
======


__Skyboxes__ are a wrapper around your entire scene that shows what the world looks like beyond your geometry.


![](../uploads/Main/Inspector-Skybox.png) 


Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Tint Color__ |The tint color|
|__Exposure__ |Adjusts the brightness of the skybox.|
|__Rotation__ |Changes the rotation of the skybox around the positive y axis.|
|__Front, etc__ |The textures used for each face of the cube used to store the skybox. Note that it is important to get these textures into the correct slot.|


Details
-------


Skyboxes are rendered around the whole scene in order to give the impression of complex scenery at the horizon. Internally skyboxes are rendered after all opaque objects; and the mesh used to render them is either a box with six textures, or a tessellated sphere.

To implement a Skybox create a skybox material. Then add it to the scene by using the Window->Lighting menu item and specifying your skybox material as the Skybox on the Scene tab.

Adding the Skybox __Component__ to a Camera is useful if you want to override the default Skybox. E.g. You might have a split screen game using two Cameras, and want the Second camera to use a different Skybox. To add a Skybox Component to a Camera, click to highlight the Camera and go to __Component-&gt;Rendering-&gt;Skybox__.

If you want to create a new Skybox, [use this guide](HOWTO-UseSkybox).


![](../uploads/Main/SkyboxWindow.png) 

Hints
-----



* If you have a Skybox assigned to a Camera, make sure to set the Camera's __Clear mode__ to Skybox.
* It's a good idea to match your Fog color to the color of the skybox. Fog color can be set in the Lighting window.
