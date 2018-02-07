#Legacy Network Reference Guide


Networking is a very large, detailed topic. In Unity, it is extremely simple to create network functionality. However, it is still best to understand the breadth and depth involved with creating any kind of network game. This section explains the fundamentals of networking and the Unity-specific implementations of these concepts. If you are new to networking then it is highly recommended that you read this guide in detail before attempting to create a network game.

The [High Level Overview](net-HighLevelOverview) is a good place to start or to refresh your knowledge of networking in general. From there, the [Unity Networking Elements](net-UnityNetworkElements) page takes the discussion to Unity's implementation of the general concepts.

Unity makes extensive use of the [Network View](net-NetworkView) component to share data over networks and so it is very important to understand how this operates. One of the functions provided by Network Views is [Remote Procedure Calls](net-RPCDetails) or **RPC**. This enables you to call a function on one or more remote machines which may be clients or servers.

Regarding the maintenance of information between networked computers, [State Synchronization](net-StateSynchronization) is a method of regularly updating a specific set of data across two or more game instances running on the network. Another subject is tracking which computer owns or controls which objects in the shared environment. [Network Instantiation](net-NetworkInstantiate) can be used to handle this task, although there are alternatives you can use when you need more control.

Discovering a computer is sometimes a matter of someone setting up a server machine and then inviting other players directly to participate. Where games offer anonymous or mass participation, a [Master Server](net-MasterServer) can be used as a place to advertise a game session and allow people to join. A master server can also use a technique called _NAT punchthrough_ to ensure players can always connect, even when firewalls are in operation.

Reducing the amount of data transferred between computers will tend to improve performance; the page on [minimizing bandwidth](net-MinimizingBandwidth) gives advice on how to achieve these optimizations.

On mobile devices, the Unity networking API is much the same as on desktop machines and so networked games will often work with little or no modification. The [Mobile Networking](MobileNetworking) page addresses some of the issues and performance considerations that do occur with mobile devices.
