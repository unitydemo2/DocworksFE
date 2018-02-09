NetworkClient 
==============

NetworkClient is a HLAPI class that manages a network connection to a server - in this case a NetworkServer. It can be used to send messages to the server and receive messages from the server. The NetworkClient also helps manage spawned network objects, and routing of RPC message and network events.



Properties
----------

|**_Property:_** ||**_Function:_** |
|:---|:---|:---|
|__serverIP__ ||The IP address of the server that this client is connected to.|
|__serverPort__ ||The port of the server that this client is connected to.|
|__connection__ ||The NetworkConnection object this client is using.|
|__handlers__ ||The set of registered message handler functions.|
|__numChannels__ ||The number of configured NetworkTransport QoS channels.|
|__isConnected__ ||True if the client is connected to a server.|
|__allClients__ ||List of active network clients (static).|
|__active__ ||True if any network clients are active (static).|
