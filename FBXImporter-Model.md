# Models

Model files that are placed in the Assets folder in your Unity project are automatically imported and stored as Unity Assets.

A model file can contain a 3D model, such as a character, a building, or a piece of furniture. The model is imported as multiple Assets. In the Project window, the main imported object is a model Prefab. Usually there are also several Mesh objects that are referenced by the model Prefab.

A model file can also contain animation data, which can be used to animate this model or other models. The animation data is imported as one or more Animation Clips.

![A [Mesh Filter](class-MeshFilter) together with the [Mesh Renderer](class-MeshRenderer) makes the model appear on screen](../uploads/Main/MeshExample40.png) 


## Import settings for Meshes

The __Import Settings__ for a model file is displayed in the __Model__ tab of the FBX importer's Inspector window when the model is selected. These affect the **Mesh**, its **Normals**, and the imported **Materials**. Settings are applied per Asset on disk, so if you need Assets with different settings, make (and rename accordingly) a duplicate file.

|**_Property_** ||**_Function_** |
|:---|:---|:---|
|**Meshes** |||
|__Scale Factor__ ||Unity's physics system expects 1 meter in the game world to be 1 unit in the imported file. If you prefer to model at a different scale then you can compensate for it here. Defaults for different 3D packages are as follows:<br/> .fbx, .max, .jas, .c4d = **0.01**<br/> .mb, .ma, .lxo, .dxf, .blend, .dae = **1** <br/>.3ds = **0.1**|
|__Use File Scale__ ||Tick the checkbox to use the default model scaling, or untick to use a custom scaling value for your model. Unity's physics system expects 1 meter in the game world to be 1 unit in the imported file. If you prefer to model at a different scale then you can compensate for it here. |
|&nbsp;&nbsp;&nbsp;&nbsp;File Scale || Use this value field to set the scale you want to use for your model. |
|__Mesh Compression__ ||Increasing this value reduces the file size of the Mesh, but might introduce irregularities. It's best to turn it up as high as possible without the Mesh looking too different from the uncompressed version. This is useful for [optimizing game size](ReducingFilesize).|
|__Read/Write Enabled__ ||If enabled, Mesh data is kept in memory so that a custom script can read and change it. Disabling this option saves memory, because Unity can unload a copy of Mesh data in the game. However, in certain cases when the Mesh is used with a [Mesh Collider](class-MeshCollider), this option must be enabled. These cases include: <br/>- Negative scaling (for example, (-1, 1, 1)). <br/>- Shear transform (for example, when a rotated Mesh has a scaled parent transform).|
|__Optimize Mesh__ ||Tick this checkbox if you want Unity to determine the order in which triangles are listed in the Mesh.|
|__Import Blendshapes__ ||Tick this checkbox if you want Unity to allow BlendShapes to be imported with your Mesh.|
|__Generate Colliders__ ||If this is enabled, your Meshes are imported with Mesh Colliders automatically attached. This is useful for quickly generating a collision Mesh for environment geometry, but should be avoided for geometry you are moving. |
| __Keep Quads__ || Unity can import any type of polygon ( triangle to N-gon ). Polygons that have more than 4 vertices are always converted to triangles. Quads are only converted to triangles if "Keep Quads" is off. Quads might be preferable over polygons when using Tessellation shaders. See documentation on [Surface Shader Tessellation](SL-SurfaceShaderTessellation) for more information. |
|__Weld Vertices__ ||Tick this checkbox to combine vertices that share the same position in space. This optimizes the vertex count on Meshes by reducing their overall number. This checkbox is ticked by default. <br/><br/>Note that there is also a `WeldVertices` parameter on the [ModelImporter](ScriptRef:ModelImporter.html) class, which does the same thing via scripting. <br/><br/>In some cases, you might need to switch this optimization off when importing your Meshes; for example, if you have constructed your Mesh in such a way that you intentionally have duplicate vertices which occupy the same position, and you want to use scripting to read or manipulate the individual vertex or triangle data. . |
|__Swap UVs__ ||Tick this checkbox if lightmapped objects are picking up the wrong UV channels. This swaps your primary and secondary UV channels.|
|__Generate Lightmap UVs__ ||Tick this checkbox if you want Unity to create a second UV channel to be used for Lightmapping. See documentation on [Lightmapping](GIIntro) for more information.|
|**Normals & Tangents** |||
|__Normals__ ||Defines if and how normals should be calculated. This is useful for [optimizing game size](ReducingFilesize). |
||__Import__ |Default option. Imports normals from the file. |
||__Calculate__ |Calculates normals based on __Smoothing angle__. If selected, the __Smoothing Angle__ becomes enabled. |
||__None__ |Disables normals. Use this option if the Mesh is neither normal mapped nor affected by realtime lighting. |
|__Tangents__ ||Defines if and how tangents and binormals should be calculated. This is useful for [optimizing game size](ReducingFilesize). |
||__Import__ |Imports tangents and binormals from the file. This option is available only for FBX, Maya and 3dsMax files and only when normals are imported from the file. |
||__Calculate__ |Default option. Calculates tangents and binormals. This option is available only when normals are either imported or calculated. |
||__None__ |Disables tangents and binormals. The Mesh has no Tangents, so won't work with normal-mapped shaders. |
|__Smoothing Angle__ ||Sets how sharp an edge has to be in order to be treated as a hard edge. It is also used to split normal map tangents. |
|__Split Tangents__ ||Enable this if normal map lighting is broken by seams on your Mesh. This usually only applies to characters. |
|**Materials** |||
|__Import Materials__ ||Disable this if you don't want Materials to be generated. By default, a diffuse Material is used instead. |
|__Material Naming__ ||Use this to define how Unity Materials are named: |
||__By Base Texture Name__ |The name of the diffuse Texture of the imported Material that is used to name the Material in Unity. When a diffuse Texture is not assigned to the Material, Unity uses the name of the imported Material. |
||__From Model's Material__ |The name of the imported Material is used for naming the Unity Material. |
||__Model Name + Model's Material__ |The name of the model file in combination with the name of the imported Material is used for naming the Unity Material. |
|__Material Search__ ||Use this to define where Unity tries to locate existing Materials using the name defined by the __Material Naming__ option: |
||__Local__ |Unity tries to find existing Materials in the "local" Materials folder only (that is, the _Materials_ subfolder, which is the same folder as the model file). |
||__Recursive-Up__ |Unity tries to find existing Materials in all Materials subfolders in all parent folders up to the Assets folder. |
||__Everywhere__ |Unity tries to find existing Materials in all Unity project folders. |


<br/>

---

* <span class="page-edit"> 2017-05-18  <!-- include IncludeTextAmendPageNoEdit --></span>

* <span class="page-history">Functionality of Keep Quads documented in 5.6</span>
