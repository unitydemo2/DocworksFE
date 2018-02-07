#Uploading raw data to an HTTP server (PUT)

Some modern web applications prefer that files be uploaded via the HTTP PUT verb. For this scenario, Unity provides the `UnityWebRequest.PUT` function.

This function takes two arguments. The first argument is a string and specifies the target URL for the request. The second argument may be either a string or a byte array, and specifies the payload data to be sent to the server.


Function signatures:

````
WebRequest.Put(string url, string data);
WebRequest.Put(string url, byte[] data);
````

##Details

* This function creates a ``UnityWebRequest`` and sets the content type to ``application/octet-stream``.
* This function attaches a standard ``DownloadHandlerBuffer`` to the ``UnityWebRequest``. As with the POST functions, you can use this to return result data from your applications.
* This function stores the input upload data in a standard ``UploadHandlerRaw`` object and attaches it to the ``UnityWebRequest``. As a result, if using the `byte[]` function, changes made to the byte array performed after the ``UnityWebRequest.PUT`` call are not reflected in the data uploaded to the server.

##Example

```
using UnityEngine;
using UnityEngine.Networking;
using System.Collections;
 
public class MyBehavior : MonoBehaviour {
    void Start() {
        StartCoroutine(Upload());
    }
 
    IEnumerator Upload() {
        byte[] myData = System.Text.Encoding.UTF8.GetBytes("This is some test data");
        UnityWebRequest www = UnityWebRequest.Put("http://www.my-server.com/upload", myData);
        yield return www.SendWebRequest();
 
        if(www.isNetworkError || www.isHttpError) {
            Debug.Log(www.error);
        }
        else {
            Debug.Log("Upload complete!");
        }
    }
}
```