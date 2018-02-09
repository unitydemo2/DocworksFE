#Retrieving text or binary data from an HTTP Server (GET)

To retrieve simple data such as textual data or binary data from a standard HTTP or HTTPS web server, use the `UnityWebRequest.GET` call. This function takes a single string as an argument, with the string specifying the URL from which data is retrieved.

This function is analogous to the standard WWW constructor:

````
WWW myWww = new WWW("http://www.myserver.com/foo.txt");
// ... is analogous to ...
UnityWebRequest myWr = UnityWebRequest.Get("http://www.myserver.com/foo.txt");
````

##Details

* This function creates a ``UnityWebRequest`` and sets the target URL to the string argument. It sets no other custom flags or headers.
* By default, this function attaches a standard ``DownloadHandlerBuffer`` to the ``UnityWebRequest``. This handler buffers the data received from the server and make it available to your scripts when the request is complete.
* By default, this function attaches no ``UploadHandler`` to the ``UnityWebRequest``. You can attach one manually if you wish.

##Example

````
using UnityEngine;
using System.Collections;
using UnityEngine.Networking;
 
class MyBehaviour: MonoBehaviour {
    void Start() {
        StartCoroutine(GetText());
    }
 
    IEnumerator GetText() {
        UnityWebRequest www = UnityWebRequest.Get("http://www.my-server.com");
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