Lightmapping Quickstart
=======================


This is an introductory description of lightmapping in Unity. For more advanced topics see the [in-depth description of lightmapping in Unity](GlobalIllumination)

Unity has a fully integrated lightmapper &ndash; **[Beast](http://www.illuminatelabs.com/products/beast)** by Illuminate Labs. This means that Beast will bake lightmaps for your scene based on how your scene is set up within Unity, taking into account meshes, materials, textures and lights. It also means that lightmapping is an integral part of the rendering engine - once your lightmaps are created you don't need to do anything else, they will be automatically picked up by the objects.


![](../uploads/Main/LightmapEditor-ApartmentScene.png) 

Preparing the scene and baking the lightmaps
--------------------------------------------


Selecting **__Window__ &ndash;&gt; __Lighting__** from the menu will open the Lightmapping window:


1. Make sure any mesh you want to be lightmapped has proper UVs for lightmapping. The easiest way is to choose the **__Generate Lightmap UVs__** option in [mesh import settings](FBXImporter-Model).
1. In the **__Object__** pane mark any Mesh Renderer, Skinned Mesh Renderer or Terrain as **__static__** &ndash; this will tell Unity, that those objects won't move nor change and they can be lightmapped.

![](../uploads/Main/LightmapperObject40.png) 

1. To control the resolution of the lightmaps, go to the **__Bake__** pane and adjust the **__Resolution__** value. (To have a better understanding on how you spend your lightmap texels, look at the small **__Lightmap Display__** window within the __Scene View__ and select **__Show Resolution__**).

![](../uploads/Main/LightmapperBakeAndShowResolution40.png) 

1. Press **__Bake__**
1. A progress bar appears in Unity Editor's status bar, in the bottom right corner.
1. When baking is done, you can see all the baked lightmaps at the bottom of the Lightmap Editor window.

Scene and game views will update - your scene is now lightmapped!

Tweaking Bake Settings
----------------------


Final look of your scene depends a lot on your lighting setup and bake settings. Let's take a look at an example of some basic settings that can improve lighting quality.

This is a basic scene with a couple of cubes and one point light in the centre. The light is casting hard shadows and the effect is quite dull and artificial. 

![](../uploads/Main/LightmappedCubesTut1.png) 

Selecting the light and opening the __Object__ pane of the __Lightmapping__ window exposes __Shadow Radius__ and __Shadow Samples__ properties. Setting Shadow Radius to 1.2, Shadow Samples to 100 and re-baking produces soft shadows with wide penumbra - our image already looks much better. 

![](../uploads/Main/LightmappedCubesTut2.png) 


We can take the scene one step further by enabling Global Illumination and adding a Sky Light. In the __Bake__ pane we set the number of __Bounces__ to 1 and the __Sky Light Intensity__ to 0.5. The result is much softer lighting with subtle diffuse interreflection effects (color bleeding from the green and blue cubes) - much nicer and it's still only 3 cubes and a light!

![](../uploads/Main/LightmappedCubesTut3.png) 


Lightmapping In-Depth
---------------------


For more information about the various lightmapping-related settings, please refer to the [in-depth description of lightmapping in Unity](GlobalIllumination).
