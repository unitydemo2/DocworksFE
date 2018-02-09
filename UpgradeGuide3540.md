Upgrading to Unity 4.0
===================================



GameObject active state
-----------------------


Unity 4.0 changes how the active state of GameObjects is handled. GameObject's active state is now inherited by child GameObjects, so that any GameObject which is inactive will also cause its children to be inactive. We believe that the new behavior makes more sense than the old one, and should have always been this way. Also, the upcoming new GUI system heavily depends on the new 4.0 behavior, and would not be possible without it. Unfortunately, this may require some work to fix existing projects to work with the new Unity 4.0 behavior, and here is the change:

###The old behavior:


* Whether a GameObject is active or not was defined by its __.active__ property.
* This could be queried and set by checking the __.active__ property.
* A GameObject's active state had no impact on the active state of child GameObjects. If you want to activate or deactivate a GameObject and all of its children, you needed to call __GameObject.SetActiveRecursively__.
* When using __SetActiveRecursively__ on a GameObject, the previous active state of any child GameObject would be lost. When you deactivate and then activated a GameObject and all its children using __SetActiveRecursively__, any child which had been inactive before the call to __SetActiveRecursively__, would become active, and you had to manually keep track of the active state of children if you want to restore it to the way it was.
* Prefabs could not contain any active state, and were always active after prefab instantiation.

###The new behavior:


* Whether a GameObject is active or not is defined by its own __.activeSelf__ property, and that of all of its parents. The GameObject is active if its own __.activeSelf__ property and that of all of its parents is __true__. If any of them are __false__, the GameObject is inactive.
* This can be queried using the __.activeInHierarchy__ property.
* The __.activeSelf__ state of a GameObject can be changed by calling __GameObject.SetActive__. When calling __SetActive (false)__ on a previously active GameObject, this will deactivate the GameObject and all its children. When calling __SetActive (true)__ on a previously inactive GameObject, this will activate the GameObject, if all its parents are active. Children will be activated when all their parents are active (i.e., when all their parents have __.activeSelf__ set to __true__).
* This means that __SetActiveRecursively__ is no longer needed, as active state is inherited from the parents. It also means that, when deactivating and activating part of a hierarchy by calling __SetActive__, the previous active state of any child GameObject will be preserved.
* Prefabs can contain active state, which is preserved on prefab instantiation.

###Example:

You have three GameObjects, A, B and C, so that B and C are children of A. 

* Deactivate C by calling __C.SetActive(false)__.
* Now, __A.activeInHierarchy == true__, __B.activeInHierarchy == true__ and __C.activeInHierarchy == false__.
* Likewise, __A.activeSelf == true__, __B.activeSelf == true__ and __C.activeSelf == false__.
* Now we deactivate the parent A by calling __A.SetActive(false)__.
* Now, __A.activeInHierarchy == false__, __B.activeInHierarchy == false__ and __C.activeInHierarchy == false__.
* Likewise, __A.activeSelf == false__, __B.activeSelf == true__ and __C.activeSelf == false__.
* Now we activate the parent A again by calling __A.SetActive(true)__.
* Now, we are back to __A.activeInHierarchy == true__, __B.activeInHierarchy == true__ and __C.activeInHierarchy == false__.
* Likewise, __A.activeSelf == true__, __B.activeSelf == true__ and __C.activeSelf == false__.

###The new active state in the editor

To visualize these changes, in the Unity 4.0 editor, any GameObject which is inactive (either because it's own __.activeSelf__ property is set to __false__, or that of one of it's parents), will be greyed out in the hierarchy, and have a greyed out icon in the inspector. The GameObject's own __.activeSelf__ property is reflected by it's active checkbox, which can be toggled regardless of parent state (but it will only activate the GameObject if all parents are active).

###How this affects existing projects:


* To make you aware of places in your code where this might affect you, the __GameObject.active__ property and the __GameObject.SetActiveRecursively()__ function have been deprecated.
* They are, however still functional. Reading the value of __GameObject.active__ is equivalent to reading __GameObject.activeInHierarchy__, and setting __GameObject.active__ is equivalent to calling __GameObject.SetActive()__. Calling __GameObject.SetActiveRecursively()__ is equivalent to calling __GameObject.SetActive()__ on the GameObject and all of it's children.
* Exiting scenes from 3.5 are imported by setting the __selfActive__ property of any GameObject in the scene to it's previous __active__ property.
* As a result, any project imported from previous versions of Unity should still work as expected (with compiler warnings, though), as long as it does not rely on having active children of inactive GameObjects (which is no longer possible in Unity 4.0).
* If your project relies on having active children of inactive GameObjects, you need to change your logic to a model which works in Unity 4.0.



Changes to the asset processing pipeline
----------------------------------------


During the development of 4.0 our asset import pipeline has changed in some significant ways internal in order to improve performance, memory usage and determinism. For the most part these changes does not have an impact on the user with one exception: Objects in assets are not made persistent until the very end of the import pipeline and any previously imported version of an assets will be completely replaced.

The first part means that during post processing you cannot get the correct references to objects in the asset and the second part means that if you use the references to a previously imported version of the asset during post processing do store modification those modifications will be lost.

###Example of references being lost because they are not persistent yet
Consider this small example:



````
public class ModelPostprocessor : AssetPostprocessor
{
    public void OnPostprocessModel(GameObject go)
    {
        PrefabUtility.CreatePrefab("Prefabs/" + go.name, go);
    }
}


````

In Unity 3.5 this would create a prefab with all the correct references to the meshes and so on because all the meshes would already have been made persistent, but since this is not the case in Unity 4.0 the same post processor will create a prefab where all the references to the meshes are gone, simply because Unity 4.0 does not yet know how to resolve the references to objects in the original model prefab. To correctly copy a modelprefab in to prefab you should use __OnPostProcessAllAssets__ to go through all imported assets, find the modelprefab and create new prefabs as above.


###Example of references to previously imported assets being discarded
The second example is a little more complex but is actually a use case we have seen in 3.5 that broke in 4.0. Here is a simple __ScriptableObject__ with a references to a mesh.



````
public class Referencer : ScriptableObject
{
    public Mesh myMesh;	
}


````

We use this __ScriptableObject__ to create an asset with references to a mesh inside a model, then in our post processor we take that reference and give it a different name, the end result being that when we have reimported the model the name of the mesh will be what the post processor determines.



````
public class Postprocess : AssetPostprocessor
{
	public void OnPostprocessModel(GameObject go)
	{
		Referencer myRef = (Referencer)AssetDatabase.LoadAssetAtPath("Assets/MyRef.asset", typeof(Referencer));
		myRef.myMesh.name = "AwesomeMesh";
	}
}


````

This worked fine in Unity 3.5 but in Unity 4.0 the already imported model will be completely replaced, so changing the name of the mesh from a previous import will have no effect. The Solution here is to find the mesh by some other means and change its name. What is most important to note is that in Unity 4.0 you should ONLY modify the given input to the post processor and not rely on the previously imported version of the same asset.



Mesh Read/Write option
----------------------


Unity 4.0 adds a "Read/Write Enabled" option in [Mesh](class-FBXImporter) import settings. When this option is turned off, it saves memory since Unity can unload a copy of mesh data in the game.

However, if you are scaling or instantiating meshes at runtime with a non-uniform scale, you may have to enable "Read/Write Enabled" in their import settings. The reason is that non-uniform scaling requires the mesh data to be kept in memory. Normally we detect this at build time, but when meshes are scaled or instantiated at runtime you need to set this manually. Otherwise they might not be rendered in game builds correctly.

Mesh optimization
-----------------


The Model Importer in Unity 4.0 has become better at mesh optimization. The "Mesh Optimization" checkbox in the Model Importer in Unity 4.0 is now enabled by default, and will reorder the vertices in your Mesh for optimal performance. You may have some post-processing code or effects in your project which depend on the vertex order of your meshes, and these might be broken by this change. In that case, turn off "Mesh Optimization" in the Mesh importer. Especially, if you are using the SkinnedCloth component, mesh optimization will cause your vertex weight mapping to change. So if you are using SkinnedCloth in a project imported from 3.5, you need to turn off "Mesh Optimization" for the affected meshes, or reconfigure your vertex weights to match the new vertex order.

Mobile input
------------


With Unity 4.0 mobile sensor input got better alignment between platforms, which means you can write less code when handling typical input on mobile platforms. Now acceleration and gyro input will follow screen orientation in the same way both on iOS and Android platforms. To take advantage of this change you should refactor your input code and remove platform and screen orientation specific code when handling acceleration and gyro input. You still can get old behavior on iOS by setting __Input.compensateSensors__ to false.
