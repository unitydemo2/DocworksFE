# Model Importer: Model

Model files that are placed in the Assets folder in your Unity project are automatically imported and stored as Unity Assets.

A model file can contain a 3D model, such as a character, a building, or a piece of furniture. The model is imported as multiple Assets. In the Project window, the main imported object is a model Prefab. Usually there are also several Mesh objects that are referenced by the model Prefab.

A model file can also contain animation data, which can be used to animate this model or other models. The animation data is imported as one or more Animation Clips.

![A [Mesh Filter](class-MeshFilter) together with the [Mesh Renderer](class-MeshRenderer) makes the model appear on screen](../uploads/Main/MeshExample40.png) 


## Import settings for Meshes

The __Import Settings__ for a model file is displayed in the __Model__ tab of the FBX importer's Inspector window when the model is selected. These affect the **Mesh** and its **Normals**. Settings are applied per Asset on disk, so if you need Assets with different settings, make (and rename accordingly) a duplicate file.

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
|__Index Format__ ||Defines the size of the mesh index buffer. **Note:** For bandwidth and memory storage size reasons, you generally want to keep __16 bit__ indices as default, and only use __32 bit__ when necessary. |
||__Auto__ |Allows Unity to choose whether to use 16 or 32 bit indices when importing a mesh, depending on the mesh vertex count. This is the default for assets added in Unity 2017.3 and onwards. |
||__16 bit__ |Makes Unity always use 16 bit indices when importing a mesh. If the mesh is larger, then it is split into <64k vertex chunks. Assets that already exist in projects made in Unity 2017.2 or previous versions will use this setting.|
||__32 bit__ |Makes Unity always use 32 bit indices when importing a mesh. This might be useful if you are doing GPU-based rendering pipelines (for example with compute shader triangle culling). This ensures that all meshes use the same index format and allows you to have simpler compute shaders, because they only need to handle one format. |
|__Weld Vertices__ ||Tick this checkbox to combine vertices that share the same position in space. This optimizes the vertex count on Meshes by reducing their overall number. This checkbox is ticked by default. <br/><br/>Note that there is also a `WeldVertices` parameter on the [ModelImporter](ScriptRef:ModelImporter.html) class, which does the same thing via scripting. <br/><br/>In some cases, you might need to switch this optimization off when importing your Meshes; for example, if you have constructed your Mesh in such a way that you intentionally have duplicate vertices which occupy the same position, and you want to use scripting to read or manipulate the individual vertex or triangle data. . |
|__Import Cameras__ ||Tick this checkbox to import cameras from your .FBX file|
|__Import Lights__ ||Tick this checkbox to import lights from your .FBX file|
|__Swap UVs__ ||Tick this checkbox if lightmapped objects are picking up the wrong UV channels. This swaps your primary and secondary UV channels.|
|__Generate Lightmap UVs__ ||Tick this checkbox if you want Unity to create a second UV channel to be used for Lightmapping. See documentation on [Lightmapping](GIIntro) for more information.|
|**Normals & Tangents** |||
|__Normals__ ||Defines if and how normals should be calculated. This is useful for [optimizing game size](ReducingFilesize). |
||__Import__ |Default option. Imports normals from the file. |
||__Calculate__ |Calculates normals based on __Smoothing angle__. If selected, the __Smoothing Angle__ becomes enabled. |
||__None__ |Disables normals. Use this option if the Mesh is neither normal mapped nor affected by realtime lighting. |
| __Normals Mode__ || Define how the normals are calculated by Unity. This is only available when __Normals__ is set to __Calculate__. |
|| __Unweighted Legacy__ | The legacy method of computing the normals (prior to version 2017.1).  In some cases it gives slightly different results compared to the current implementation. It is the default for all FBX prefabs imported before the migration of the project to the latest version of Unity. |
|| __Unweighted__ | The normals are not weighted. |
|| __Area Weighted__ | The normals are weighted by face area. |
|| __Angle Weighted__ | The normals are weighted by the vertex angle on each face. |
| | __Area and Angle Weighted__ | Default option. The normals are weighted by both the face area and the vertex angle on each face. This is the default option.|
|__Tangents__ ||Defines if and how tangents and binormals should be calculated. This is useful for [optimizing game size](ReducingFilesize). |
||__Import__ |Imports tangents and binormals from the file. This option is available only for FBX, Maya and 3dsMax files and only when normals are imported from the file. |
||__Calculate__ |Default option. Calculates tangents and binormals. This option is available only when normals are either imported or calculated. |
||__None__ |Disables tangents and binormals. The Mesh has no Tangents, so won't work with normal-mapped shaders. |
|__Smoothing Angle__ ||Sets how sharp an edge has to be in order to be treated as a hard edge. It is also used to split normal map tangents. |
|__Split Tangents__ ||Enable this if normal map lighting is broken by seams on your Mesh. This usually only applies to characters. |

##Light and Camera import

###Cameras
The following Camera properties are supported when importing Cameras from an .FBX file:

* Field of View

* Projection mode ( Orthographic or perspective )

* Near plane distance 

* Far plane distance

###Lights

The following light types are supported: 

* Omni
* Spot
* Directional
* Area

The following light properties are supported:

* Intensity
* Color
* Range (the FarAttenuationEndValue is used if UseFarAttenuation is enabled)
* Spot Angle (spot lights only)

---

* <span class="page-edit"> 2017-09-04  <!-- include IncludeTextAmendPageSomeEdit --></span>

* <span class="page-edit"> 2017-12-05  <!-- include IncludeTextAmendPageSomeEdit --></span>

* <span class="page-history">Existing (pre Unity 5.6) functionality of __Keep Quads__ first documented in User Manual 5.6</span>

* <span class="page-history">__Normals Mode__, __Light__ and __Camera__ import options added in Unity [2017.1](../Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>

* <span class="page-history">__Materials__ tab added in [2017.2](https://docs.unity3d.com/2017.2/Documentation/Manual/30_search.html?q=newin20172) <span class="search-words">NewIn20172</span></span>

* <span class="page-history">__Index Format__ property added in [2017.3](https://docs.unity3d.com/2017.3/Documentation/Manual/30_search.html?q=newin20173) <span class="search-words">NewIn20173</span></span>
