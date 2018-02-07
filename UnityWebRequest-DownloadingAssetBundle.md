#Downloading an AssetBundle from an HTTP server (GET)

To download an AssetBundle from a remote server, you can use `UnityWebRequest.GetAssetBundle`. This function streams data into an internal buffer, which decodes and decompresses the AssetBundle's data on a worker thread.

The function's arguments take several forms. In its simplest form, it takes only the URL from which the AssetBundle should be downloaded. You may optionally provide a checksum to verify the integrity of the downloaded data.

Alternately, if you wish to use the AssetBundle caching system, you may provide either a version number or a Hash128 data structure. These are identical to the version numbers or `Hash128 objects` provided to the old system via `WWW.LoadFromCacheOrDownload`.

##Details

* This function creates a `UnityWebRequest` and sets the target URL to the supplied URL argument. It also sets the HTTP verb to `GET`, but sets no other flags or custom headers.
* This function attaches a `DownloadHandlerAssetBundle` to the `UnityWebRequest`. This download handler has a special `assetBundle` property, which can be used to extract the AssetBundle once enough data has been downloaded and decoded to permit access to the resources inside the AssetBundle.
* If you supply a version number or `Hash128` object as arguments, it also passes those arguments to the `DownloadHandlerAssetBundle`. The download handler then employs the caching system.

##Example

````
using UnityEngine;
using UnityEngine.Networking;
using System.Collections;
 
public class MyBehaviour : MonoBehaviour {
    void Start() {
        StartCoroutine(GetAssetBundle());
    }
 
    IEnumerator GetAssetBundle() {
        UnityWebRequest www = UnityWebRequest.GetAssetBundle("http://www.my-server.com/myData.unity3d");
        yield return www.SendWebRequest();
 
        if(www.isNetworkError || www.isHttpError) {
            Debug.Log(www.error);
        }
        else {
            AssetBundle bundle = DownloadHandlerAssetBundle.GetContent(www);
        }
    }
}
````