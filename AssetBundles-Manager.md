# AssetBundle Manager

The AssetBundle Manager, which can be downloaded [here](https://www.assetstore.unity3d.com/en/#!/content/45836), is a tool made by Unity to make using AssetBundles more streamlined.

Downloading and importing the AssetBundle Manager package not only adds a new API calls for loading and using AssetBundles but it adds some Editor functionality to streamline the workflow as well.  This functionality can be found under the Assets menu option. 

This new section will contain the following options:

## Simulation Mode

Enabling Simulation Mode allows the AssetBundle Manager to work with AssetBundles but does not require the bundles themselves actually be built.  The editor looks to see what Assets  have been assigned to AssetBundles and uses the Assets directly, instead of actually pulling them from an AssetBundle.

The main advantage of using Simulation Mode is that Assets can be modified, updated, added, and deleted without the need to re-build and deploy the AssetBundles every time.  

It is worth noting that AssetBundle Variants do not work with Simulation Mode.  If you need to use variants, Local AssetBundle Server is the option you need.

## Local AssetBundle Server

The AssetBundle Manager can also start a Local AssetBundle Server which can be used to test AssetBundles in the editor or in local builds (including Mobile).

The stipulation to getting the Local AssetBundle Server to work is that you must create a folder called AssetBundles in the root directory of your project which is the same level as the Assets folder.  Such as:

![](../uploads/Main/AssetBundles-Manager-4.png)

After you create the folder you’ll need to build your AssetBundles to this folder.  To do this, select Build AssetBundles from the new menu options.  This will build them to that directory for you.

Now you have your AssetBundles built (or have decided to use Simulation Mode) and are ready to start loading AssetBundles.  Let’s look at the new API calls available to us through the AssetBundle Manager.

## AssetBundleManager.Initialize()

This function loads the AssetBundleManifest object.  You’ll need to call this before you start loading in Assets using the AssetBundle Manager.  In a very simplified example, initializing the AssetBundle Manager could look like this:

```
IEnumerator Start()

{
	yield return StartCoroutine(Initialize());
}
IEnumerator Initialize()
{
	var request = AssetBundleManager.Initialize();
if (request != null)
	yield return StartCoroutine(request);
}
```

The AssetBundle Manager uses this manifest you load during the Initialize() to help with a number of features behind the scenes, including dependency management.

## Loading Assets

Let’s get right down to it.  You’re using the AssetBundle Manager, you’ve initialized it, and now you’re ready to load some Assets.  Let’s take a look at how to load the AssetBundle and instantiate an object from that bundle:

```
IEnumerator InstantiateGameObjectAsync (string assetBundleName, string assetName)

{
	// Load asset from assetBundle.
	AssetBundleLoadAssetOperation request = AssetBundleManager.LoadAssetAsync(assetBundleName, assetName, typeof(GameObject) );
	if (request == null)
		yield break;
	yield return StartCoroutine(request);
	// Get the asset.
	GameObject prefab = request.GetAsset<GameObject> ();
	if (prefab != null)
		GameObject.Instantiate(prefab);
}
```

The AssetBundle Manager performs all of it’s load operation asynchronously so it returns a load operation request that loads the bundle upon calling yield return StartCoroutine(request); From there all we need to do is call the GetAsset\<T\>() to load a game object from the AssetBundle.

## Loading Scenes

If you’ve got an AssetBundle name assigned to a scene and you need to load that scene in you’ll need to follow a slightly different code path.  The pattern is relatively the same, but with slight differences.  Here’s how to load a scene from an AssetBundle:

```
IEnumerator InitializeLevelAsync (string levelName, bool isAdditive)

{
	// Load level from assetBundle.
	AssetBundleLoadOperation request = AssetBundleManager.LoadLevelAsync(sceneAssetBundle, levelName, isAdditive);
	if (request == null)
		yield break;
	yield return StartCoroutine(request);
}
```

As you can see, loading scenes is also an asynchronous and LoadLevelAsync returns a load operation request which will need to be passed to a StartCoroutine in order to load the scene.

## Load Variants

Loading variants using the AssetBundle Manager doesn’t actually change the code need to load in the scenes or assets.  All that needs to be done is set the ActiveVariants property of the AssetBundleManager.

The ActiveVariants property is an array of strings.  Simply build an array of strings containing the names of the variants you created during assigning them to the Assets.  Here’s how to load a scene AssetBundle with the hd variant.

```
IEnumerator InitializeLevelAsync (string levelName, bool isAdditive, string[] variants)

{
	//Set the activeVariants.
	AssetBundleManager.ActiveVariants = variants;
	// Load level from assetBundle.
	AssetBundleLoadOperation request = AssetBundleManager.LoadLevelAsync(variantSceneAssetBundle, levelName, isAdditive);
	if (request == null)
		yield break;
	yield return StartCoroutine(request);
}
```

Where you’d pass in the string array you built up elsewhere in your code (perhaps from a button click or some other circumstances). This will load the bundles that match the set active variants if it is available.  

---
* <span class="page-edit">2017-05-15  <!-- include IncludeTextNewPageNoEdit --></span>


