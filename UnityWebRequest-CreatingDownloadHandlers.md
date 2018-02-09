#Creating DownloadHandlers

There are four types of `DownloadHandlers`:

* `DownloadHandlerBuffer` is used for simple data storage.
* `DownloadHandlerTexture` is used for downloading images. 
* `DownloadHandlerAssetBundle` is used for fetching AssetBundles.
* `DownloadHandlerScript` is a special class. On its own, it does nothing. However, this class can be inherited by a user-defined class. This class receives callbacks from the UnityWebRequest system, which can then be used to perform completely custom handling of data as it arrives from the network.

A specialized Download Handler for Audio clips is also available. The APIs are similar to `DownloadHandlerTexture`'s interface.

##DownloadHandlerBuffer
This Download Handler is the simplest, and handles the majority of use cases. It stores received data in a native code buffer. When the download is complete, you can access the buffered data either as an array of bytes or as a UTF8 string.

###Example

````
using UnityEngine;
using UnityEngine.Networking; 
using System.Collections;

 
class MyBehaviour: MonoBehaviour {
    void Start() {
        StartCoroutine(GetText());
    }
 
    IEnumerator GetText() {
        UnityWebRequest www = new UnityWebRequest("http://www.my-server.com");
        www.downloadHandler = new DownloadHandlerBuffer();
        yield return www.Send();
 
        if(www.isError) {
            Debug.Log(www.error);
        }
        else {
            // Show results as text
            Debug.Log(www.downloadHandler.text);
 
            // Or retrieve results as binary data
            byte[] results = www.downloadHandler.data;
        }
    }
}
````

##DownloadHandlerTexture
Instead of using a ``DownloadHandlerBuffer`` to download an image file and then creating a texture from the raw bytes using ``Texture.LoadImage``, it's more efficient to use ``DownloadHandlerTexture``.

This Download Handler stores received data in a `UnityEngine.Texture`. On download completion, it decodes JPEGs and PNGs into valid `UnityEngine.Texture objects`. Only one copy of the `UnityEngine.Texture` is created per `DownloadHandlerTexture` object. This reduces performance hits from garbage collection. The handler performs buffering, decompression and texture creation in native code. Additionally, decompression and texture creation are performed on a worker thread instead of the main thread, which can improve frame time when loading large textures.

Finally, ``DownloadHandlerTexture`` only allocates managed memory when finally creating the Texture itself, which eliminates the garbage collection overhead associated with performing the byte-to-texture conversion in script.


###Example

The following example downloads a PNG file from the internet, converts it to a Sprite, and assigns it to an [image](script-Image):

````
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.Networking; 
using System.Collections;

[RequireComponent(typeof(UnityEngine.UI.Image))]
public class ImageDownloader : MonoBehaviour {
    UnityEngine.UI.Image _img;
 
    void Start () {
        _img = GetComponent<UnityEngine.UI.Image>();
        Download("http://www.mysite.com/myimage.png");
    }
 
    public void Download(string url) {
        StartCoroutine(LoadFromWeb(url));
    }
 
    IEnumerator LoadFromWeb(string url)
    {
        UnityWebRequest wr = new UnityWebRequest(url);
        DownloadHandlerTexture texDl = new DownloadHandlerTexture(true);
        wr.downloadHandler = texDl;
        yield return wr.Send();
        if(!wr.isError) {
            Texture2D t = texDl.texture;
            Sprite s = Sprite.Create(t, new Rect(0, 0, t.width, t.height),
                                     Vector2.zero, 1f);
            _img.sprite = s;
        }
    }
}
````

##DownloadHandlerAssetBundle

The advantage to this specialized Download Handler is that it is capable of streaming data to Unity's AssetBundle system. Once the AssetBundle system has received enough data, the AssetBundle is available as a `UnityEngine.AssetBundle` object. Only one copy of the `UnityEngine.AssetBundle` object is created. This considerably reduces run-time memory allocation as well as the memory impact of loading your AssetBundle. It also allows AssetBundles to be partially used while not fully downloaded, so you can stream Assets.

All downloading and decompression occurs on worker threads.

AssetBundles are downloaded via a ``DownloadHandlerAssetBundle`` object, which has a special ``assetBundle`` property to retrieve the AssetBundle.

Due to the way the AssetBundle system works, all AssetBundle must have an address associated with them. Generally, this is the nominal URL at which they're located (meaning the URL before any redirects). In almost all cases, you should pass in the same URL as you passed to the UnityWebRequest. When using the High Level API (HLAPI), this is done for you.

###Example

````
using UnityEngine;
using UnityEngine.Networking; 
using System.Collections;
 
class MyBehaviour: MonoBehaviour {
    void Start() {
        StartCoroutine(GetAssetBundle());
    }
 
    IEnumerator GetAssetBundle() {
        UnityWebRequest www = new UnityWebRequest("http://www.my-server.com");
        DownloadHandlerAssetBundle handler = new DownloadHandlerAssetBundle(www.url, uint.MaxValue);
        www.downloadHandler = handler;
        yield return www.Send();
 
        if(www.isError) {
            Debug.Log(www.error);
        }
        else {
            // Extracts AssetBundle
            AssetBundle bundle = handler.assetBundle;
        }
    }
}
````

##DownloadHandlerScript

For users who require full control over the processing of downloaded data, Unity provides the ``DownloadHandlerScript`` class.

By default, instances of this class do nothing. However, if you derive your own classes from ``DownloadHandlerScript``, you may override certain functions and use them to receive callbacks as data arrives from the network.

**Note:** The actual downloads occur on a worker thread, but all ``DownloadHandlerScript`` callbacks operate on the main thread. Avoid performing computationally heavy operations during these callbacks.

###Functions to override

####ReceiveContentLength()

````
protected void ReceiveContentLength(long contentLength);
````
This function is called when the Content Length header is received. Note that this callback may occur multiple times if your server sends one or more redirect responses over the course of processing your UnityWebRequest.

####OnContentComplete()

````
protected void OnContentComplete();
````
This function is called when the UnityWebRequest has fully downloaded all data from the server, and has forwarded all received data to the ReceiveData callback.

####ReceiveData()

````
protected bool ReceiveData(byte[] data, long dataLength);
````
This function is called after data has arrived from the remote server, and is called once per frame. The `data` argument contains the raw bytes received from the remote server, and `dataLength` indicates the length of new data in the data array.

When not using pre-allocated data buffers, the system creates a new byte array each time it calls this callback, and `dataLength` is always equal to ``data.Length``. When using pre-allocated data buffers, the data buffer is reused, and ``dataLength`` must be used to find the number of updated bytes.

This function requires a return value of either __true__ or __false__. If you return __false__, the system immediately aborts the UnityWebRequest. If you return __true__, processing continues normally.

###Avoiding garbage collection overhead
Many of Unity's more advanced users are concerned with reducing CPU spikes due to garbage collection. For these users, the UnityWebRequest system permits the pre-allocation of a managed-code byte array, which is used to deliver downloaded data to DownloadHandlerScript's ``ReceiveData`` callback.

Using this function completely eliminates managed-code memory allocation when using DownloadHandlerScript-derived classes to capture downloaded data.

To make a ``DownloadHandlerScript`` operate with a pre-allocated managed buffer, supply a byte array to the constructor of ``DownloadHandlerScript``.

**Note:** The size of the byte array limits the amount of data delivered to the ReceiveData callback each frame. If your data arrives slowly, over many frames, you may have provided too small of a byte array.

####Example

````
using UnityEngine;
using UnityEngine.Networking; 
using System.Collections;

public class LoggingDownloadHandler : DownloadHandlerScript {

    // Standard scripted download handler - allocates memory on each ReceiveData callback
   
    public LoggingDownloadHandler(): base() {
    }

    // Pre-allocated scripted download handler
    // reuses the supplied byte array to deliver data.
    // Eliminates memory allocation.
    
    public LoggingDownloadHandler(byte[] buffer): base(buffer) {
    }

    // Required by DownloadHandler base class. Called when you address the 'bytes' property.
    
    protected override byte[] GetData() { return null; }

    // Called once per frame when data has been received from the network.
    
    protected override bool ReceiveData(byte[] data, int dataLength) {
        if(data == null || data.Length < 1) {
            Debug.Log("LoggingDownloadHandler :: ReceiveData - received a null/empty buffer");
            return false;
        }

        Debug.Log(string.Format("LoggingDownloadHandler :: ReceiveData - received {0} bytes", dataLength));
        return true;
    }

    // Called when all data has been received from the server and delivered via ReceiveData.
    
    protected override void CompleteContent() {
        Debug.Log("LoggingDownloadHandler :: CompleteContent - DOWNLOAD COMPLETE!");
    }

    // Called when a Content-Length header is received from the server.
    
    protected override void ReceiveContentLength(int contentLength) {
        Debug.Log(string.Format("LoggingDownloadHandler :: ReceiveContentLength - length {0}", contentLength));
    }
}
````

