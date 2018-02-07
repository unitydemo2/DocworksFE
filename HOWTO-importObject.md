#How do I import models from my 3D app?

There are two ways to import 3D models into Unity:

* Drag the 3D model file from your file browser straight into the Unity Project window.
* Copy the 3D model file into the Project’s Assets folder. 

Select the file in the __Project__ view and navigate to the __Model__ tab in the Inspector window to configure import options. See documentation on [Models](FBXImporter-Model) for more information about import options.

Unity supports importing models from most popular 3D applications. For more guidance on how to import from specific 3D packages, see the following pages:

* [Maya](HOWTO-ImportObjectMaya)
* [Cinema 4D](HOWTO-ImportObjectCinema4D)
* [3ds Max](HOWTO-ImportObjectMax)
* [Cheetah3D](HOWTO-ImportObjectCheetah3D)
* [Modo](HOWTO-ImportObjectModo)
* [Lightwave](HOWTO-importObjectLightwave)
* [Blender](HOWTO-ImportObjectBlender)
* [SketchUp](HOWTO-ImportObjectSketchUp)

##Textures

You must store Textures in a folder called __Textures__, placed inside the __Assets__ folder (next to the exported Mesh) within your Unity Project. This enables the Unity Editor to find the Textures and connect them to the generated Materials. For more information, see documentation on [Importing Textures](class-TextureImporter).

<!-- include 3D-formats -->

<!-- include FBXImporter-Model -->

##See also

* [Modeling optimized characters](ModelingOptimizedCharacters)
* [Mesh import settings](class-Mesh)
* [How do I fix the rotation of an imported model?](HOWTO-FixZAxisIsUp)