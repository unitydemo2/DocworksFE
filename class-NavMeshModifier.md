# NavMesh Modifier


NavMesh Modifiers adjust how a specific GameObject behaves during NavMesh baking at runtime. NavMesh Modifiers are not in the Unity standard install; see documentation on [high-level NavMesh building components](NavMesh-BuildingComponents) for information on how to access them.


To use the NavMesh Modifier component, navigate to __GameObject__ > __AI__ > __NavMesh Modifier__.

In the image below, the platform in the bottom right has a modifier attached to it that sets its __Area Type__ to __Lava__.

![A NavMesh Modifier component open in the Inspector window](../uploads/Main/class-NavMeshModifier-3.png)

The NavMesh Modifier affects GameObjects hierarchically, meaning the GameObject that the component is attached to as well as all its children are affected. Additionally, if another NavMesh Modifier is found further down the transform hierarchy, the new NavMesh Modifier overrides the one further up the hierarchy.

The NavMesh Modifier also affects the NavMesh generation process, meaning the NavMesh has to be updated to reflect any changes to NavMesh Modifiers.

|**Property:** |**Function:** |
|:---|:---|
| __Ignore From Build__| Check this tickbox to exclude the GameObject and all if its children from the build process. |
| __Override Area Type__| Check this tickbox to change the area type for the GameObject containing the Modifier and all of its children. |
| __Area Type__| Select the new area type to apply from the drop-down menu. |
| __Affected Agents__| A selection of Agents the Modifier affects. For example, you may choose to exclude certain obstacles from specific Agents.  |


<br/><br/>

---

* <span class="page-edit"> 2017-05-26  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">New feature in 5.6</span>