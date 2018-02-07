FBX export guide
================


Unity supports FBX files which can be generated from many popular 3D applications. Use these guidelines to help ensure the best results.

**Select &gt; Prepare &gt; Check Settings &gt; Export &gt; Verify &gt; Import**


###**What** do you want to export? 

Be aware of export scope e.g. meshes, cameras, lights, animation rigs, etc.


* Applications often let you export **selected objects** or a **whole scene**
* Make sure you are exporting only the objects you want to use from your scene by either exporting selected, or removing unwanted data from your scene.
* Good working practice often means keeping a working file with all lights, guides, control rigs etc. but only export the data you need with _export selected,_ an export preset or even a custom scene exporter.

###**What** do you need to include? 

Prepare your assets:


* Meshes - Remove construction history, Nurbs, Nurms, Subdiv surfaces must be converted to polygons - e.g. triangulate or quadrangulate
* Animation - Select the correct rig, check frame rate, animation length etc.
* Blend Shapes / Morphing - Make sure your Blendshapes (Maya) or Morph targets (Max) are assigned / set up the export mesh appropriately
* Textures - Make sure your textures are sourced already from your Unity project or copied into a folder called \textures in your project
* Smoothing - Check if you want smoothing groups and/or smooth mesh

###**How** do I include those elements? 

Check the FBX export settings


* Be aware of your settings in the export dialogue so that you know what to expect and can match up the FBX settings In Unity - see figs 1, 2 & 3 below
* Check Animation / Deformations / Skins / Morphs as appropriate
* Nodes, markers and their transforms can be exported
* Cameras and Lights are not currently imported in to Unity

###**Which** version of FBX are you using? 

Use the [Latest Version of FBX](http://usa.autodesk.com/adsk/servlet/pc/item?siteID=123112&id=10775855) where possible.  


* Autodesk update their FBX installer regularly and it can provide different results with different versions of their own software and other 3rd party 3D apps

* **See Advanced Options &gt; FBX file format**

* If you have any issues you can revert to [2012.2](http://usa.autodesk.com/adsk/servlet/pc/item?siteID=123112&id=18817399) if necessary


###Will it work? 

Verify your export


* Check your file size - do a sanity check on the file size (e.g. &gt;10kb?)
* Re-import your FBX into a new scene in the 3D package you use to generate it - is it what you expected?

###**Import!**


* Import into Unity
* Check FBX import settings in inspector : textures, animations, smoothing and so on.

See below for Maya FBX dialogue example:

![General, Geometry & Animation](../uploads/Main/FBX_A.png) 


![Lights, Advanced options](../uploads/Main/FBX_B.png) 
