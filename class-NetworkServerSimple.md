NetworkServerSimple 
==============

NetworkServerSimple is a High Level API (HLAPI) class that manages connections from multiple clients. While the NetworkServer class handles game-like things such as spawning, local clients, and player manager, and has a static interface, the NetworkServerSimple class is a pure network server with no game related functionality. It also has no static interface or singleton, so more than one instance can exist in a process at a time.

The NetworkServer class uses an instance of NetworkServerSimple internally to do connection management.


Properties
----------

|**_Property:_** ||**_Function:_** |
|:---|:---|:---|
|__connections__ ||The set of active connections to remote clients. This is a sparse array where NetworkConnect objects reside at the index of their connectionId. There may be nulls in this array for recently closed connections. The connection at index zero may be the connection from the local client.|
|__handlers__ ||The set of registered message handler function.|
|__networkConnectionClass__ ||The type of NetworkConnection object to create for new connections.|
|__hostTopology__ ||The host topology object that this server used to configure the transport layer.
|__listenPort__ ||The network port that the server is listening on.|
|__serverHostId__ ||The transport layer hostId associated with this server instance.|

