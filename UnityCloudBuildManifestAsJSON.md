# Build manifest as JSON 

You can access the [Unity Cloud Build manifest](UnityCloudBuildManifest) as JSON at runtime. This Asset requires either custom parsing logic or the use of a third party JSON parser.

The following example C# code demonstrates loading and parsing the build manifest with the MiniJSON parser on GitHub Gist ([gist.github.com/darktable/1411710](https://gist.github.com/darktable/1411710)):

````

using UnityEngine;
using System.Collections.Generic;
using MiniJSON;

public class MyGameObject: MonoBehavior
{
    void Start()
    {
        var manifest = (TextAsset) Resources.Load("UnityCloudBuildManifest.json");
        if (manifest != null)
        {
            var manifestDict = Json.Deserialize(manifest.text) as Dictionary<string,object>;
            foreach (var kvp in manifestDict)
            {
                // Be sure to check for null values!
                var value = (kvp.Value != null) ? kvp.Value.ToString() : "";
                Debug.Log(string.Format("Key: {0}, Value: {1}", kvp.Key, value));
            }
        }
    }
}
````
