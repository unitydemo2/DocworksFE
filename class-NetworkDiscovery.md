NetworkDiscovery 
==============

NetworkDiscovery is a class that allows Unity application using the networking system find each other on a local network.


Properties
----------

|**_Property:_** ||**_Function:_** |
|:---|:---|:---|
|__broadcastPort__ ||The port to broadcast on. |
|__broadcastKey__ ||The key to broadcast. |
|__broadcastVersion__ ||The major version to include in the broadcast. |
|__broadcastSubVersion__ ||The minor version to include in the broadcast. |
|__broadcastInterval__ ||How often in seconds to broadcast. |
|__useNetworkManager__ ||True to use NetworkManager settings for broadcasting and auto-join games found. |
|__broadcastData__ ||Custom data to include in the broadcast. |
|__showGUI__ ||True to show the default broadcast GUI in play mode. |
|__offsetX__ ||The x offset of the broadcast GUI. |
|__offsetY__ ||The y offset of the broadcast GUI. |
|__hostId__ ||The host Id being used to broadcast (read-only). |
|__running__ ||True if currently broadcasting. |
|__isServer__ ||True is broadcasting as a server. |
|__isClient__ ||True if listening for broadcasts as a client. |
|__broadcastsReceived__ ||A list of broadcast messages received. |
