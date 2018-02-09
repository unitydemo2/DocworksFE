#Using the Transport Layer API

In addition to the High Level networking API that we provide - which provides easy-to-use systems for managing your players, networked GameObjects, and other common requirements - we also give access to a lower level API called the "Transport Layer". This provides you with the ability to build your own networking systems at a lower level, which can be useful if you have more specific or advanced requirements for your game's networking.

The Transport Layer is a thin layer working on top of the operating system's sockets-based networking. It's capable of sending and receiving messages represented as arrays of bytes, and offers a number of different "quality of service" options to suit different scenarios. It is focused on flexibility and performance, and exposes an API within the UnityEngine.Networking.NetworkTransport class.

The Transport Layer supports base services for network communication. These base services include:

* Establishing Connections
* Communicating using a variety of "quality of services"
* Flow control
* Base statistics
* Additional services like communication via relay server or local discovery

The Transport Layer can use two protocols: UDP for generic communications, and WebSockets for WebGL.
To use the Transport Layer directly, the typical workflow would be as follows:

1. Initialize the Network Transport Layer
3. Configure network topology
4. Create Host
5. Start communication (handling connections and sending/receiving messages)
6. Shut down library after use.

### Initializing the Network Transport Layer

When initializing the Network Transport Layer, you can choose between the default initialization, with no arguments, or you can provide parameters which control the overall behaviour of the network layer, such as the maximum packet size and the thread timout limit.

```C#
	// Initializing the Transport Layer with no arguments (default settings)
	NetworkTransport.Init();
```


```C#
	// An example of initializing the Transport Layer with custom settings
	GlobalConfig gConfig = new GlobalConfig();
	gConfig.MaxPacketSize = 500;
	NetworkTransport.Init(gConfig);
```

In the 2nd example above, the Transport Layer is initialized with a custom "MaxPacketSize" value specified of 500. Custom Init values should only be used if you have an unusual networking environment and are familiar with the specific settings you need. As a rule of thumb, if you are developing a typical multiplayer game designed to be played across the internet, the default Init() settings with no arguments should be appropriate.

###Configuration
The next step is configuration of connection between peers. You may want to define several communication channels, each with a different quality of service level specified to suit the specific types of messages that you want to send, and their relative importance within your game.

```C#
	ConnectionConfig config = new ConnectionConfig();
	int myReiliableChannelId  = config.AddChannel(QosType.Reliable);
	int myUnreliableChannelId = config.AddChannel(QosType.Unreliable);
```

In the example above, we define two communication channels with different quality of service values. "QosType.Reliable" will deliver message and assure that the message is delivered, while "QosType.Unreliable" will send message without any assurance, but will do this faster. 

It's also possible to specify configuration settings specifically for each connection, by adjusting properties on the ConnectionConfig object. However, when making a connection from one client to another, the settings should be the same for both connected peers or the connection will fail with a `CRCMismatch` error.

###Topology
The final step of network configuration is topology definition. Network topology defines how many connections allowed and what connection configuration will used:

```C#
HostTopology topology = new HostTopology(config, 10);
```

Here we created topology which allow up to 10 connections, each of them will configured by parameters defines in previous step.

###Host creating 
As all preliminary steps have done, we can create host (open socket):

```C#
int hostId = NetworkTransport.AddHost(topology, 8888);
```

Here we add new host on port 8888 and any ip addresses. This host will support up to 10 connection, and each connection will have parameters as we defined in `config` object.

###Communication
As host created, we can start our communication. To do this we send different command to host and check its status.
There are 3 main command which we can send:

```C#
connectionId = NetworkTransport.Connect(hostId, "192.16.7.21", 8888, 0, out error);
NetworkTransport.Disconnect(hostId, connectionId, out error);
NetworkTransport.Send(hostId, connectionId, myReiliableChannelId, buffer, bufferLength,  out error);
```

1. The first command will send connect request to peer with ip "192.16.7.21" and port 8888. It will return id assigned to this connection. 
2. The second will send disconnect request, 
3. And third will send message, to connection with id equal `connectionId`, using reliable channel with id equal `myReiliableChannelId`, message should be stored in `buffer[]` and length of the message should be defined by `bufferLength`.


For checking host status you can use two functions:

```C#
NetworkTransport.Receive(out recHostId, out connectionId, out channelId, recBuffer, bufferSize, out dataSize, out error);
NetworkTransport.ReceiveFromHost(recHostId, out connectionId, out channelId, recBuffer, bufferSize, out dataSize, out error);
```

Both of them returns event, first function will return events from any host (and return host id via  `recHostId`) the second form check host with id `recHostId`. You can use any of these function inside `Update()` method:

```C#
void Update()
{
	int recHostId; 
	int connectionId; 
	int channelId; 
	byte[] recBuffer = new byte[1024]; 
	int bufferSize = 1024;
	int dataSize;
	byte error;
	NetworkEventType recData = NetworkTransport.Receive(out recHostId, out connectionId, out channelId, recBuffer, bufferSize, out dataSize, out error);
	switch (recData)
	{
		case NetworkEventType.Nothing:         //1
			break;
		case NetworkEventType.ConnectEvent:    //2
			break;
		case NetworkEventType.DataEvent:       //3
			break;
		case NetworkEventType.DisconnectEvent: //4
			break;
	}
}
```
* Point 1: No interesting events have been returned.
* Point 2: Connection event come in. It can be new connection, or it can be response on previous connect command:

```C#
myConnectionId = NetworkTransport.Connect(hostId, "192.16.7.21", 8888, 0, out error);
NetworkEventType recData = NetworkTransport.Receive(out recHostId, out connectionId, out channelId, recBuffer, bufferSize, out dataSize, out error);
switch (recData)
{
	case NetworkEventType.ConnectEvent: 
		if(myConnectionId == connectionId)
			//my active connect request approved
		else
			//somebody else connect to me
		break;
	//...	
}
```
* Point 3: Data received. In this case `recHostId` will define host, connectionId will define connection, `channelId` will define channel; `dataSize` will define size of the received data. If `recBuffer` is big enough to contain data, data will be copied in the buffer. If not, `error` will contain `MessageToLong` error and you will need reallocate buffer and call this function again.
* Point 4: Disconnection signal come in. It can be signal that established connection has been disconnected or that your connect request is failed.

```C#
myConnectionId = NetworkTransport.Connect(hostId, "192.16.7.21", 8888, 0, out error);
NetworkEventType recData = NetworkTransport.Receive(out recHostId, out connectionId, out channelId, recBuffer, bufferSize, out dataSize, out error);
switch (recData)
{
	case NetworkEventType. DisconnectEvent: 
		if(myConnectionId == connectionId)
			//cannot connect by some reason see error
		else
			//one of the established connection has been disconnected
		break;
	\\...	
}
```
###WebGL support
WebSocket on client has been supported. 
For client side, all steps described above (including topology and configuration) should be the same. Web clients can connect to server only, where server is standalone player (Win, Mac or Linux only).
On server you should call 

```C#
NetworkTransport.AddWebsocketHost(topology, port, ip);
```

Where `ip` address is listening address, you can pass null as ip address in this case host will listen all network interfaces. Server can support only one Websocket Host and in the same time, it can handle generic hosts too:

```C#
NetworkTransport.AddWebsocketHost(topology, 8887, null);
NetworkTransport.AddHost(topology, 8888);
```

Will open tcp socket handling web socket protocol on port 8887 and udp socket handling genetic protocol on port 8888.
