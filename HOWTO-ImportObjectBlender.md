Importing Objects From Blender
==============================


Unity natively imports Blender files. This works under the hood by using the Blender FBX exporter.

To get started, save your **.blend** file in your project's Assets folder. When you switch back into Unity, the file is imported automatically and will show up in the __Project View__.

To see your model in Unity, drag it from the Project View into the __Scene View__.

If you modify your **.blend** file, Unity will automatically update whenever you save.

Unity currently imports
-----------------------


1. All nodes with position, rotation and scale. Pivot points and Names are also imported.
1. Meshes with vertices, polygons, triangles, UVs, and normals.
1. Bones
1. Skinned Meshes
1. Animations

See [Using Blender and Rigify](BlenderAndRigify) for more details of how to import animated, boned characters into Unity for use with Mecanim.

Requirements
------------


* You need to have Blender version 2.60 or later (in some earlier versions of Blender the FBX export was broken).
* Textures and diffuse color are not assigned automatically. Manually assign them by dragging the texture onto the mesh in the Scene View in Unity.
