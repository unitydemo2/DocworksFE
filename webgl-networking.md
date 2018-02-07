WebGL Networking
================

No direct socket access
-----------------------

Due to security implications, JavaScript code does not have direct access to IP Sockets to implement network connectivity. As a result, the .NET networking classes (ie, everything in the `System.Net` namespace, particularly `System.Net.Sockets`) are non-functional in WebGL. The same applies to Unity's old `UnityEngine.Network*` classes, which are not available when building for WebGL.

If you need to use Networking in WebGL, you currently have the options to use the `WWW` or `UnityWebRequest` classes in Unity or the new [Unity Networking](UNetOverview) features which support WebGL, or to implement your own networking using WebSockets or WebRTC in JavaScript.

Using the WWW or WebRequest classes in WebGL
--------------------------------------------

The __[WWW](ScriptRef:WWW.html)__ and __[UnityWebRequest](ScriptRef:Networking.UnityWebRequest)__ classes are supported in WebGL. They are implemented using the `XMLHttpRequest` class in JavaScript, using the browser to handle WWW requests. This imposes some security restrictions on accessing cross-domain resources. Basically any WWW request to a server which is different from the server hosting the WebGL content needs to be authorized by the server you are trying to access. To access cross-domain WWW resources in WebGL, the server you are trying to access needs to authorize this using CORS. 

If you try to access content using `WWW` or `UnityWebReqest`, and the remote server does not have CORS set up or configured correctly, you will see an error like this in the browser console:

````
Cross-Origin Request Blocked: The Same Origin Policy disallows reading the remote resource at http://myserver.com/. This can be fixed by moving the resource to the same domain or enabling CORS.
````

CORS stands for Cross-Origin Resource Sharing, and is documented [here](http://www.w3.org/TR/cors/). Basically, the server needs to add some `Access-Control` headers to the http responses it sends out, which will tell browsers that it is allowed to let web pages access the content on the server. Here's an example of a header setup, which would allow Unity WebGL to access resources on a web server from any origin, with common request headers and using the http `GET`, `POST` or `OPTIONS` methods:

````
"Access-Control-Allow-Credentials": "true",
"Access-Control-Allow-Headers": "Accept, X-Access-Token, X-Application-Name, X-Request-Sent-Time",
"Access-Control-Allow-Methods": "GET, POST, OPTIONS",
"Access-Control-Allow-Origin": "*",
````

Note that WWW.responseHeaders is limited to a subset of the actual response headers, according to [7.1.1](http://www.w3.org/TR/cors/#handling-a-response-to-a-cross-origin-request) of the CORS specification.

Also note that XMLHttpRequest does not allow streaming of data, thus the WWW class on WebGL will only process any data once the download has finished (so AssestBundles cannot be decompressed and loaded while downloading as on other platforms).

### Do not block on WWW or WebRequest downloads

Do not use code which blocks on a WWW or WebRequest download, like this:

```
while(!www.isDone) {}
```

Blocking on WWW or WebRequest downloads does not work on Unity WebGL. Because WebGL is single threaded, and because the `XMLHttpRequest` class in JavaScript is asynchronous, your download never finishes unless you return control to the browser; instead, your content deadlocks. Instead, use a [Coroutine](Coroutines) and a `yield` statement to wait for the download to finish.

Using Unity Networking
----------------------

[Unity Networking](UNetOverview) supports WebGL by enabling communication via the WebSockets protocol. See __[Networking.NetworkManager.useWebSockets](ScriptRef:Networking.NetworkManager-useWebSockets.html)__.

Using Web Sockets or WebRTC from JavaScript 
-------------------------------------------

As written above, direct access to IP Sockets is not possible in WebGL. However, if you need networking capabilities beyond the WWW class, it is possible to use Web Sockets or WebRTC, both networking protocols supported by browsers. Web Sockets has wider support, but WebRTC allows p2p connections between browsers and unreliable connections. Neither of these protocols are exposed through built-in APIs in Unity yet, but it is possible to use a [JavaScript plugin](webgl-interactingwithbrowserscripting) to implement this. A sample of a plugin which implements WebSocket networking in Unity WebGL can be found on [AssetStore](https://www.assetstore.unity3d.com/en/#!/content/38367e).
