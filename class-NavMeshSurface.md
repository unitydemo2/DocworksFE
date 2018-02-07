# NavMesh Surface

The NavMesh Surface component represents the walkable area for a specific [NavMesh Agent](class-NavMeshAgent) type, and defines a part of the Scene where a NavMesh should be built. 

The NavMesh Surface component is not in the standard Unity install; see documentation on [high-level NavMesh building components](NavMesh-BuildingComponents) for information on how to access it. 

To use the NavMesh Surface component, navigate to __GameObject__ > __AI__ > __NavMesh Surface__. This creates an empty GameObject with a NavMesh Surface component attached to it. A Scene can contain multiple NavMesh Surfaces.

You can add the NavMesh Surface component to any GameObject. This is useful for when you want to use the GameObject parenting [Hierarchy](Hierarchy) to define which GameObjects contribute to the NavMesh.

![A NavMesh Surface component open in the Inspector window](../uploads/Main/class-NavMeshSurface-0.png)

| __Property__| __Function__ |
|:---|:---| 
| __Agent Type__| The [NavMesh Agent](nav-CreateNavMeshAgent) type using the NavMesh Surface. Use for bake settings and matching the NavMesh Agent to proper surfaces during pathfinding.<br/>- Humanoid<br/>- Ogre |
| __Collect Objects__| Defines which GameObjects to use for baking.<br/>- __All__ – Use all active GameObjects (this is the default option).<br/>- __Volume__ – Use all active GameObjects overlapping the bounding volume.<br/>- __Children__ – Use all active GameObjects which are children of the NavMesh Surface component. |
| __Include Layers__| Define the layers on which GameObjects are included in the [bake](nav-BuildingNavMesh). In addition to __Collect Objects__, this allows for further exclusion of specific GameObjects from the bake (for example, effects or animated characters).<br/> This is set to __Everything__ by default, but you can toggle  following options on (denoted by a tick) or off individually:<br/>- __Nothing__ (automatically unticks all other options, turning them off)<br/>- __Everything__ (automatically ticks all other options, turning them on)<br/>- __Default__ <br/>- __TransparentFX__ <br/>- __Ignore [Raycast](Raycasters)__<br/> - __Water__ <br/> - __UI__ |
| __Use Geometry__| Select which geometry to use for baking.<br/>- __Render Meshes__ – Use geometry from Render Meshes and [Terrains](terrain-UsingTerrains).<br/>-  __Physics [Colliders](CollidersOverview)__ – Use geometry from Colliders and Terrains. Agents can move closer to the edge of the physical bounds of the environment with this option than they can with the __Render Meshes__ option. |

Use the main settings for the NavMesh Surface component to filter the input geometry on a broad scale. Fine tune how Unity treats input geometry on a per-GameObject basis, using the [NavMesh Modifier component](class-NavMeshModifier). 

The baking process automatically excludes GameObjects that have a NavMesh Agent or NavMesh Obstacle. They are dynamic users of the NavMesh, and so do not contribute to NavMesh building.

## Advanced settings

![The NavMesh Surface Advanced settings panel](../uploads/Main/class-NavMeshSurface-1.png)

The Advanced settings section allows you to customize the following additional parameters:

| __Property__| __Function__ |
|:---|:---| 
| __Default Area__ | Defines the area type generated when building the NavMesh.<br/> - __Walkable__ (this is the default option)<br/> - __Not Walkable__<br/> - __Jump__ <br/> Use the [NavMesh Modifier](class-NavMeshModifier) component to modify the area type in more detail. |
| __Override Voxel Size__ | Controls how accurately Unity processes the input geometry for NavMesh baking (this is a tradeoff inbetween speed and accuracy). Check the tickbox to enable. The default is unchecked (disabled).<br/> 3 voxels per Agent radius (6 per diameter) allows the capture of narrow passages, such as doors, while maintaining a quick baking time. For big open areas, using 1 or 2 voxels per radius speeds up baking. Tight indoor spots are better suited to smaller voxels, for example 4 to 6 voxels per radius. More than 8 voxels per radius does not usually provide much additional benefit. |
| __Override Tile Size__ | In order to make the bake process parallel and memory efficient, the Scene is divided into tiles for baking. The white lines visible on the NavMesh are tile boundaries. <br/> The default tile size is 256 voxels, which provides a good tradeoff between memory usage and NavMesh fragmentation. <br/> To change this default tile size, check this tickbox and, in the __Tile Size__ field,  enter the number of voxels you want the Tile Size to be. <br/> The smaller the tiles, the more fragmented the NavMesh is. This can sometimes cause non-optimal paths. NavMesh carving also operates on tiles. If you have a lot of obstacles, you can often speed up carving by making the tile size smaller (for example around 64 to 128 voxels). If you plan to bake the NavMesh at runtime, using a smaller tile size to keep the maximum memory usage low. |
| __Build Height Mesh__| Not supported. |

## Advanced Debug Visualization

![Input Geometry, Regions, Polygonal Mesh Detail and Raw Contours shown after building the NavMesh with debug options](../uploads/Main/class-NavMeshSurface-ADV-0.png)

![Nav Mesh Surface Inspector with Debug Visualization options](../uploads/Main/class-NavMeshSurface-ADV-1.png)

Use the settings in the __Debug Visualization__ section  to  diagnose any problems encountered during the NavMesh building process. The different tickboxes show each step of the NavMesh building process, including input scene voxelization (__Input Geometry__), region splitting (__Regions__), contour generation (__Contours__) and the NavMesh polygons (__Polygon Meshes__).

---

* <span class="page-edit"> 2017-09-14  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">New feature in 5.6</span>

* <span class="page-history">New Advanced Debug Visualization added in [2017.2](https://docs.unity3d.com/2017.2/Documentation/Manual/30_search.html?q=newin20172) <span class="search-words">NewIn20172</span></span>