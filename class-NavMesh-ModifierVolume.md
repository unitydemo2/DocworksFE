# NavMesh Modifier Volume

The NavMesh Modifier Volume component is not in the Unity standard install; see documentation on [high-level NavMesh building components](NavMesh-BuildingComponents) for information on how to access it. 

NavMesh Modifier Volume marks a defined area as a certain type (for example, __Lava__ or __Door__). Whereas [NavMesh Modifier](class-NavMeshModifier) marks certain GameObjects with an area type. NavMesh Modifier Volume allows you to change an area type locally based on a specific volume.

To use the NavMesh Modifier Volume component, navigate to __GameObject__ > __AI__ > __NavMesh Modifier Volume__.

NavMesh Modifier Volume is useful for marking certain areas of walkable surfaces that might not be represented as separate geometry, for example danger areas. You can also use It to make certain areas non-walkable.

The NavMesh Modifier Volume also affects the NavMesh generation process, meaning the NavMesh has to be updated to reflect any changes to NavMesh Modifier Volumes.

![A NavMesh Modifier Volume component open in the Inspector window](../uploads/Main/class-NavMesh-ModifierVolume-4.png)

| __Property__| __Function__ |
|:---|:---| 
| __Size__| Dimensions of the NavMesh Modifier Volume, defined by XYZ measurements.  |
| __Center__| The center of the NavMesh Modifier Volume relative to the GameObject center, defined by XYZ measurements. |
| __Area Type__| Describes the area type to which the NavMesh Modifier Volume applies.<br/> - __Walkable__ (this is the default option)<br/> - __Not Walkable__<br/> - __Jump__ |
| __Affected Agents__| A selection of Agents the NavMesh Modifier Volume affects. For example, you may choose to make the selected NavMesh Modifier Volume a danger zone for specific Agent types only.<br/>- __None__<br/> - __All__ (this is the default option)<br/> - __Humanoid__<br/> - __Ogre__ |

<br/><br/>

---

* <span class="page-edit"> 2017-05-26  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">New feature in 5.6</span>