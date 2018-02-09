#Creating UploadHandlers

Currently, only one type of upload handler is available: `UploadHandlerRaw`. This class accepts a data buffer at construction time. This buffer is copied internally into native code memory and then used by the `UnityWebRequest` system when the remote server is ready to accept body data.

Upload Handlers also accept a Content Type string. This string is used for the value of the UnityWebRequest's `Content-Type` header if you set no `Content-Type` header on the UnityWebRequest itself. If you manually set a `Content-Type` header on the UnityWebRequest object, the `Content-Type` on the Upload Handler object is ignored.

If you do not set a `Content-Type` on either the UnityWebRequest or the `UploadHandler`, the system defaults to setting a `Content-Type` of `application/octet-stream`.

##Example

````
byte[] payload = new byte[1024];
// ... fill payload with data ...

UnityWebRequest wr = new UnityWebRequest("http://www.mysite.com/data-upload");
UploadHandler uploader = new UploadHandlerRaw(payload);

// Sends header: "Content-Type: custom/content-type";
uploader.contentType = "custom/content-type";

wr.uploadHandler = uploader;
````