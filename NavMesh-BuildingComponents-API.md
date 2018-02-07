# NavMesh building components API

[NavMesh](nav-NavigationSystem) building [components](UsingComponents) provide you with additional controls for building (also known as [baking](nav-BuildingNavMesh)) and using NavMeshes at run time and in the Unity Editor.

NavMesh Modifiers are not in the Unity standard install; see documentation on [high-level NavMesh building components](NavMesh-BuildingComponents) for information on how to access them.

### NavMeshSurface

#### Properties

* `agentTypeID` – ID describing the Agent type the NavMesh should be built for. 
* `collectObjects` – Defines how input geometry is collected from the Scene, one of `UnityEngine.AI.CollectObjects:`
    * `All` – Use all objects in the scene.
    * `Volume` – Use all GameObjects in the Scene that touch the bounding volume (see `size` and `center`) 
    * `Children` – use all objects which are children to the Game Object where the NavMesh Surface is attached to.
* `size` – Dimensions of the build volume. The size is not affected by scaling. 
* `center` – Center of the build volume relative to the transform center.
* `layerMask` – Bitmask defining the layers on which the GameObjects must be to be included in the baking. 
* `useGeometry` – Defines which geometry is used for baking, one of `UnityEngine.NavMeshCollectGeometry`:
    * `RenderMeshes` – Use geometry from render meshes and terrains
    * `PhysicsColliders` – Use geometry from colliders and terrains.
* `defaultArea` – Default area type for all input geometries, unless otherwise specified.
* `ignoreNavMeshAgent` – True if GameObjects with a Nav Mesh Agent component should be ignored as input.
* `ignoreNavMeshObstacle` – True if GameObjects with a Nav Mesh Obstacle component should be ignored as input.
* `overrideTileSize` – True if tile size is set.
* `tileSize` – Tile size in voxels (the component description includes information on how to choose tile size).
* `overrideVoxelSize` – True if the voxel size is set.
* `voxelSize` – Size of the voxel in world units (the component description includes information on how to choose tile size).
* `buildHeightMesh` – Not implemented.
* `bakedNavMeshData` – Reference to the NavMeshData the surface uses, or null if not set.
* `activeSurfaces` – List of all active NavMeshSurfaces.

__Note:__ The above values affect how the bake results, and so you must call `Bake()` to include them.

#### Public Functions

* `void Bake ()`

Bakes a new NavMeshData based on the parameters set on NavMesh Surface. The data can be accessed via `bakedNavMeshData`.

### NavMesh Modifier

#### Properties

* `overrideArea` – True if the modifier overrides area type.
* `area` – New area type to apply.
* `ignoreFromBuild` – True if the GameObject which contains the modifier and its children should be not be used to NavMesh baking.
* `activeModifiers` – List of all active NavMeshModifiers.

#### Public Functions

* `bool AffectsAgentType(int agentTypeID)`

Returns true if the modifier applies to the specified Agent type, otherwise false. 

### NavMesh Modifier Volume

#### Properties

* `size` – Size of the bounding volume in local space units. Transform affects the size. 
* `center` – Center of the bounding volume in local space units. Transform affects the center.
* `area ` – Area type to apply for the NavMesh areas that are inside the bounding volume.

#### Public Functions

* `bool AffectsAgentType(int agentTypeID)`

Returns true of the the modifier applies for the specified Agent type. 

### NavMesh Link

#### Properties

* `agentTypeID` – The type of Agent that can use the link.
* `startPoint` – Start point of the link in local space units. Transform affects the location.
* `endPoint` – End point of the link in local space units. Transform affects the location.
* `width` – Width of the link in world length units.
* `bidirectional` – If true, the link can be traversed both ways. If false, the link can be traversed only from start to end.
* `autoUpdate` – If true, the link updates the end points to follow the transform of the GameObject every frame.
* `area ` – Area type of the link (used for pathfinding cost).

#### Public Functions

* `void UpdateLink()`

Updates the link to match the associated transform. This is useful for updating a link, for example after changing the transform position, but is not necessary if the `autoUpdate` property is enabled. However calling `UpdateLink` can have a much smaller performance impact if you rarely change the link transform.

<br/><br/>
---

* <span class="page-edit"> 2017-05-26  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">New feature in 5.6</span>

