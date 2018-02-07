How do I Make a Skybox?
=======================


A __Skybox__ is a 6-sided cube that is drawn behind all graphics in the game. Here are the steps to create one:


* Make 6 textures that correspond to each of the 6 sides of the skybox and put them into your project's __Assets__ folder.
* For each texture you need to change the wrap mode from __Repeat__ to __Clamp__. If you don't do this colors on the edges will not match up:  

![](../uploads/Main/SkyboxWrapmode.png)

* Create a new __Material__ by choosing __Assets-&gt;Create-&gt;Material__ from the menu bar.
* Select the shader drop-down in the top of the __Inspector__, choose __Skybox/6 Sided__.
* Assign the 6 textures to each texture slot in the material. You can do this by dragging each texture from the __Project View__ onto the corresponding slots. 

![](../uploads/Main/SkyboxMaterial.png)

In this screen shot the textures have been taken from the 4.x StandardAssets/Skyboxes/Textures folder.  Note that these textures are already used in SkyBoxes.

To Assign the skybox to the scene you're working on:

* Choose __Window-&gt;Lighting__ from the menu bar.
* In the window that appears select the Scene tab.
* Drag the new Skybox Material to the __Skybox__ slot. 

![](../uploads/Main/SkyboxRenderSettings.png)

