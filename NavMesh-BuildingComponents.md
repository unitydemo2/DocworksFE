# NavMesh building components

[NavMesh](nav-NavigationSystem) building [components](UsingComponents) provide you with additional controls for building (also known as [baking](nav-BuildingNavMesh)) and using NavMeshes at run time and in the Unity Editor. 

The high-level NavMesh building components listed below are not supplied with the standard Unity Editor installer which you download from the [Unity store](https://store.unity.com/). Instead, download them from [the Unity Technologies GitHub](https://github.com/Unity-Technologies/NavMeshComponents) and install them separately.

There are four high-level components to use with NavMesh:

* [NavMesh Surface](class-NavMeshSurface) - Use for building and enabling a NavMesh surface for one type of Agent.

* [NavMesh Modifier](class-NavMeshModifier) - Use for affecting the NavMesh generation of NavMesh area types based on the transform hierarchy.

* [NavMeshModifierVolume](class-NavMesh-ModifierVolume) - Use for affecting the NavMesh generation of NavMesh area types based on volume.

* [NavMeshLink](class-NavMeshLink) - Use for connecting the same or different NavMesh surfaces for one type of Agent.


See also documentation on [Mesh-BuildingComponents-API](NavMesh-BuildingComponents-API).

For more information on Agent types, refer to documentation on [creating NavMesh Agents](nav-CreateNavMeshAgent).

For more details about NavMesh area types, see documentation on [NavMesh areas](nav-AreasAndCosts).



## Creating high-level NavMesh building components

To install the high-level NavMesh building components:

1. [Download and install](https://store.unity.com/) Unity 5.6 or later.

2. Clone or download the repository from [the NavMesh Components page](https://github.com/Unity-Technologies/NavMeshComponents) on the Unity Technologies GitHub by clicking on the green __Clone or download__ button.

3. Open the NavMesh Components Project using Unity, or alternatively copy the contents of the  *A**ssets/NavMeshComponents* folder to an existing Project.

Find additional examples in the *Assets/Examples* folder.

__Note:__ Make sure to back up your Project before installing high-level NavMesh building components.

<br/><br/>

--------

* <span class="page-edit"> 2017-05-26  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">New feature in 5.6</span>