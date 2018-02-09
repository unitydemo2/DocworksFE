#Retrieving a Texture from an HTTP Server (GET)

To retrieve a Texture file from a remote server, you can use `UnityWebRequest.Texture.` This function is very similar to `UnityWebRequest.GET` but is optimized for downloading and storing textures efficiently.

This function takes a single string as an argument. The string specifies the URL from which you wish to download an image file for use as a Texture.

##Details

* This function creates a `UnityWebRequest` and sets the target URL to the string argument. This function sets no other flags or custom headers.
* This function attaches a `DownloadHandlerTexture` object to the `UnityWebRequest`. DownloadHandlerTexture is a specialized Download Handler which is optimized for storing images which are to be used as Textures in the Unity Engine. Using this class significantly reduces memory reallocation compared with downloading raw bytes and creating a Texture manually in script.
* By default, this function attaches on Upload Handler. You can add one manually if you wish.

##Example

````
using UnityEngine;
using System.Collections;
using UnityEngine.Networking;
 
class MyBehaviour: MonoBehaviour {
    void Start() {
        StartCoroutine(GetTexture());
    }
 
    IEnumerator GetTexture() {
        UnityWebRequest www = UnityWebRequest.GetTexture("http://www.my-server.com/image.png");
        yield return www.Send();

        if(www.isError) {
            Debug.Log(www.error);
        }
        else {
            Texture myTexture = ((DownloadHandlerTexture)www.downloadHandler).texture;
        }
    }
}
````

Alternatively, you can implement GetTexture using a helper getter:

````
    IEnumerator GetTexture() {
        UnityWebRequest www = UnityWebRequest.GetTexture("http://www.my-server.com/image.png");
        yield return www.Send();

        Texture myTexture = DownloadHandlerTexture.GetContent(www);
    }
````
