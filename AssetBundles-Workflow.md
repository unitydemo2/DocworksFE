# AssetBundle Workflow

To get started with AssetBundles, follow these steps. More detailed information about each piece of the workflow can be found in the other pages in this section of documentation.

## Assigning Assets to AssetBundles

To assign a given Asset to an AssetBundle, follow these steps:

1. Select the asset you want to assign to a bundle from your Project View
2. Examine the object in the inspector
3. At the bottom of the inspector, you should see a section to assign AssetBundles and Variants:
4. The left-hand drop down assigns the AssetBundle while the right-hand drop down assigns the variant
5. Click the left-hand drop down where it says "None" to reveal the currently registered AssetBundle names
6. If none have yet been created, you’ll see a list like that in the image above
7. Click "New…" to create a new AssetBundle
8. Type in the desired AssetBundle name. Note that AssetBundle names do support a type of folder structure depending on what you type.  To add sub folders, separate folder names by a "/". For example: AssetBundle name "environment/forest" will create a bundle named forest under an environment sub folder
9. Once you’ve selected or created an AssetBundle name, you can repeat this process for the right hand drop down to assign or create a Variant name, if you desire.  Variant names are not required to build the AssetBundles

To read more information on AssetBundle assignments and accompanying strategies, see documentation on [Preparing Assets for AssetBundles](#AssetBundles-Preparing)
.

## Build the AssetBundles

Create a folder called Editor in the Assets folders, and place a script with the following contents in the folder:

```
using UnityEditor;

public class CreateAssetBundles
{
	[MenuItem("Assets/Build AssetBundles")]
	static void BuildAllAssetBundles()
	{
		string assetBundleDirectory = "Assets/AssetBundles";
		if(!Directory.Exists(assetBundleDirectory)
{
	Directory.CreateDirectory(assetBundleDirectory);
}
BuildPipeline.BuildAssetBundles(assetBundleDirectory, BuildAssetBundleOptions.None, BuildTarget.Standalone);
	}
}
```

This script will create a menu item at the bottom of the Assets menu called "Build AssetBundles" that will execute the code in the function associated with that tag.  When you click Build AssetBundles a progress bar will appear with a build dialogue.  This will take all the assets you labeled with an AssetBundle name in and place them in a folder at the path defined by assetBundleDirectory.

For more detail about what this code is doing, see documentation on [Building AssetBundles](#AssetBundles-Building).

## Upload AssetBundles to off-site storage

This step is unique to each user and not a step Unity can tell you how to do.  If you plan on uploading your AssetBundles to a third party hosting site, do that here.  If you’re doing strictly local development and intend to have all of your AssetBundles on disk, skip to the next step.

## Loading AssetBundles and Assets

For users intending to load from local storage, you’ll be interested in the AssetBundles.LoadFromFile API.  Which looks like this:

```
public class LoadFromFileExample extends MonoBehaviour {
	function Start() {
		var myLoadedAssetBundle = AssetBundle.LoadFromFile(Path.Combine(Application.streamingAssetsPath, "myassetBundle"));
		if (myLoadedAssetBundle == null) {
			Debug.Log("Failed to load AssetBundle!");
			return;
		}
		var prefab = myLoadedAssetBundle.LoadAsset.<GameObject>("MyObject");
		Instantiate(prefab);
	}
}
```

`LoadFromFile` takes the path of the bundle file.

If you’re hosting your AssetBundles yourself and need to download them into your game, you’ll be interested in the UnityWebRequest API.  Here’s an example:

```
IEnumerator InstantiateObject()

    {
        string uri = "file:///" + Application.dataPath + "/AssetBundles/" + assetBundleName;        UnityEngine.Networking.UnityWebRequest request = UnityEngine.Networking.UnityWebRequest.GetAssetBundle(uri, 0);
        yield return request.Send();
        AssetBundle bundle = DownloadHandlerAssetBundle.GetContent(request);
        GameObject cube = bundle.LoadAsset<GameObject>("Cube");
        GameObject sprite = bundle.LoadAsset<GameObject>("Sprite");
        Instantiate(cube);
        Instantiate(sprite);
    }
```

`GetAssetBundle(string, int)` takes the uri of the location of the AssetBundle and the version of the bundle you want to download. In this example we’re still pointing to a local file but the string uri could point to any url you have your AssetBundles hosted at.

The UnityWebRequest has a specific handle for dealing with AssetBundles, `DownloadHandlerAssetBundle`, which gets the AssetBundle from the request.

Regardless of the method you use, you’ll now have access to the AssetBundle object.  From that object you’ll need to use `LoadAsset<T>(string)` which takes the type, `T`, of the asset you’re attempting to load and the name of the object as a string that’s inside the bundle. This will return whatever object you’re loading from the AssetBundle.  You can use these returned objects just like any object inside of Unity. For example, if you want to create a GameObject in the scene, you just need to call `Instantiate(gameObjectFromAssetBundle)`.  

For more information on APIs that load AssetBundles, see documentation on [Using AssetBundles Natively](#AssetBundles-Native).

----
* <span class="page-edit">2017-05-15  <!-- include IncludeTextNewPageNoEdit --></span>
