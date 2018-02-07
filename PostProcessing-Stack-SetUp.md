## Setting up the post-processing stack

For optimal post-processing results it is recommended that you work in the Linear color-space with HDR enabled. Using the deferred rendering path is also recommended (as required for some effects, such as [Screen Space Reflection](PostProcessing-ScreenSpaceReflection)).

First you need to add the Post Processing Behaviour script to your camera. You can do that by selecting your camera and use one of the following ways:

* Drag the _PostProcessingBehaviour.cs_ script from the project window to the camera.

* Use the menu __Component__ > __Effects__ > __Post Processing Behaviour__.

* Use the __Add Component__ button in the Inspector.

![Adding a Post-Processing Behaviour script](../uploads/Main/PostProcessing-Stack-SetUp-0.png)

You will now have a behaviour configured with an empty profile. The next step is to create a custom profile using one of the following ways:

* Right-click in your project window and select __Create__ > __Post-Processing Profile__.

* Use the menu __Assets__ > __Create__ > __Post-Processing Profile__.

This will create a new asset in your project.

Post-Processing Profiles are project assets and can be shared easily between scenes / cameras, as well as between different projects or on the Asset Store. This makes creating presets easier (ie. high quality preset for desktop or lower settings for mobile).

Selecting a profile will show the inspector window for editing the profile settings.

![Newly created post-processing profile](../uploads/Main/PostProcessing-Stack-SetUp-1.png)

To assign the profile to the behaviour you can drag it from the project panel to the component or use the object selector in the inspector.

![Post-processing profile assigned to the Behaviour script](../uploads/Main/PostProcessing-Stack-SetUp-2.png)

With the profile selected, you can use the checkbox on each effect in the inspector to enable or disable individual effects. You'll find more information about each effect in their individual documentation pages.

![Bloom effect enabled](../uploads/Main/PostProcessing-Stack-SetUp-3.png)

---

* <span class="page-edit"> 2017-05-24  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">New feature in 5.6</span>