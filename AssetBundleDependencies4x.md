Managing Asset Dependencies in Unity 4
===========================

*In versions of Unity earlier than Unity 5, assets dependencies had to be defined using editor scripts alone. (In Unity 5 we provide tools in the editor to assign assets to specific Bundles and dependency handling is automatic). This information is provided for those working on legacy projects in Unity 4, and speaks assuming you are using Unity 4.*

Any given asset in a bundle may depend on other assets. For example, a model may incorporate materials which in turn make use of textures and shaders. It is possible to include all an asset's dependencies along with it in its bundle. However, several assets from different bundles may all depend on a common set of other assets (eg, several different models of buildings may use the same brick texture). If a separate copy of a shared dependency is included in each bundle that has objects using it, then redundant instances of the assets will be created when the bundles are loaded. This will result in wasted memory.

To avoid such wastage, it is possible to separate shared dependencies out into a separate bundle and simply reference them from any bundles with assets that need them. First, the referencing feature needs to be enabled with a call to [BuildPipeline.PushAssetDependencies](ScriptRef:BuildPipeline.PushAssetDependencies.html). Then, the bundle containing the referenced dependencies needs to be built. Next, another call to PushAssetDependencies should be made before building the bundles that reference the assets from the first bundle. Additional levels of dependency can be introduced using further calls to PushAssetDependencies. The levels of reference are stored on a stack, so it is possible to go back a level using the corresponding [BuildPipeline.PopAssetDependencies](ScriptRef:BuildPipeline.PopAssetDependencies.html) function. The push and pop calls need to be balanced including the initial push that happens before building.

At runtime, you need to load a bundle containing dependencies before any other bundle that references them. For example, you would need to load a bundle of shared textures before loading a separate bundle of materials that reference those textures.

Asset IDs
---------


If you anticipate needing to rebuild asset bundles that are part of a dependency chain then you should build them with the [BuildAssetBundleOptions.DeterministicAssetBundle](ScriptRef:BuildAssetBundleOptions.DeterministicAssetBundle.html) option enabled. This guarantees that the internal ID values used to identify assets will be the same each time the bundle is rebuilt.

When building the asset bundle with this method, the objects in it are assigned a 32 bit hash code that is calculated using the name of the asset bundle file, the GUID of the asset and the local id of the object in the asset. For that reason make sure to use the same file name when rebuilding. Also note that having a lot of objects might cause hash collisions preventing Unity from building the asset bundle.

Shaders dependencies
--------------------


Whenever shaders are directly referenced as parameters in [BuildPipeline.BuildAssetBundle](ScriptRef:BuildPipeline.BuildAssetBundle.html), or indirectly with the option [BuildAssetBundleOptions.CollectDependencies](ScriptRef:BuildAssetBundleOptions.CollectDependencies.html) the shader's code is included with the asset bundle. This could cause a problem if you use BuildAssetBundle alone to create several asset bundles, since referenced shaders will be included in every generated bundle. There could be conflicts, i.e. when you mix different versions of a shader, so you will have to rebuild all your bundles after modifying the shaders. The shader's code will also increase the size of bundles. To avoid these problems you can use [BuildPipeline.PushAssetDependencies](ScriptRef:BuildPipeline.PushAssetDependencies.html) to separate shaders in a single bundle, and that will allow you to update the shader bundle only. As an example of how to achieve this workflow, you can create a prefab that includes references to the required shaders:

###C# Example


````
using UnityEngine;

public class ShadersList : MonoBehaviour {
	public Shader[] list;
}


````

Create an empty object, assign the script, add the shaders to the list and create the prefab, i.e. "ShadersList". Then you can create an exporter that generates all the bundles and updates the bundle of shaders:

###C# Example


````
using UnityEngine;
using UnityEditor;

public class Exporter : MonoBehaviour {
	
	[MenuItem("Assets/Export all asset bundles")]
	static void Export() {
		BuildAssetBundleOptions options = 
			BuildAssetBundleOptions.CollectDependencies | 
			BuildAssetBundleOptions.CompleteAssets | 
			BuildAssetBundleOptions.DeterministicAssetBundle;
		
		BuildPipeline.PushAssetDependencies();
		BuildPipeline.BuildAssetBundle(AssetDatabase.LoadMainAssetAtPath("Assets/ShadersList.prefab"), null, "Data/ShadersList.unity3d", options);
			
		BuildPipeline.PushAssetDependencies();
		BuildPipeline.BuildAssetBundle(AssetDatabase.LoadMainAssetAtPath("Assets/Scene1.prefab"), null, "Data/Scene1.unity3d", options);
		BuildPipeline.BuildAssetBundle(AssetDatabase.LoadMainAssetAtPath("Assets/Scene2.prefab"), null, "Data/Scene2.unity3d", options);		
		
		BuildPipeline.PopAssetDependencies();
		BuildPipeline.PopAssetDependencies();
	}
	
	[MenuItem("Assets/Update shader bundle")]
	static void ExportShaders() {
		BuildAssetBundleOptions options = 
			BuildAssetBundleOptions.CollectDependencies | 
			BuildAssetBundleOptions.CompleteAssets | 
			BuildAssetBundleOptions.DeterministicAssetBundle;
		
		BuildPipeline.PushAssetDependencies();
		BuildPipeline.BuildAssetBundle(AssetDatabase.LoadMainAssetAtPath("Assets/ShadersList.prefab"), null, "Data/ShadersList.unity3d", options);
		
		BuildPipeline.PopAssetDependencies();
	}
}


````

Bear in mind that you must load the shader bundle first. One drawback of this method is that the option [BuildAssetBundleOptions.DeterministicAssetBundle](ScriptRef:BuildAssetBundleOptions.DeterministicAssetBundle.html) can produce conflicts due to colliding hashes when the amount of objects is too large. In this case the build will fail, and it won't be possible to update the shader bundle alone. In this case you will have to remove that option and rebuild all the asset bundles.

