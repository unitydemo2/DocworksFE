#Networking Overview

**Related tutorials**: [Multiplayer Networking](https://unity3d.com/learn/tutorials/topics/multiplayer-networking)

There are two kinds of users for the Networking feature:

* Users making a Multiplayer game with Unity. These users should start with the [NetworkManager](UNetManager) or the [High Level API](UNetUsingHLAPI).
* Users building network infrastructure or advanced multiplayer games. These users should start with the [NetworkTransport API](UNetUsingTransport).

##High level scripting API

Unity's networking has a "high-level" scripting API (which we'll refer to as the HLAPI). Using this means you get access to commands which cover most of the common requirements for multiuser games without needing to worry about the "lower level" implementation details. The HLAPI allows you to:

* Control the networked state of the game using a "Network Manager".
* Operate "client hosted" games, where the host is also a player client.
* Serialize data using a general-purpose serializer.
* Send and receive network messages.
* Send networked commands from clients to servers.
* Make remote procedure calls (RPCs) from servers to clients.
* Send networked events from servers to clients.

##Engine and Editor integration

Unity's networking is integrated into the engine and the editor, allowing you to work with components and visual aids to build your multiplayer game. It provides:

* A [NetworkIdentity](ScriptRef:Networking.NetworkIdentity.html) component for networked objects.
* A [NetworkBehaviour](ScriptRef:Networking.NetworkBehaviour.html) for networked scripts.
* Configurable automatic synchronization of object transforms.
* Automatic synchronization of script variables.
* Support for placing networked objects in Unity scenes.
* [Network components](UNetReference.html)

##Internet Services

Unity offers [Internet Services](UnityMultiplayerSettingUp) to support your game throughout production and release, which includes:

* Matchmaking service
* Create matches and advertise matches.
* List available matches and join matches.
* Relay server
* Game-play over internet with no dedicated server.
* Routing of messages for participants of matches.

##NetworkTransport real-time transport layer

We include a [Real-Time Transport Layer](UNetUsingTransport) that offers:

* Optimized UDP based protocol.
* Multi-channel design to avoid head-of-line blocking issues
* Support for a variety of levels of Quality of Service (QoS) per channel.
* Flexible network topology that supports peer-to-peer or client-server architectures.

##Sample Projects

You can also dig into our multiplayer sample projects to see how these features are used together. The following sample projects can be found within [this Unity Forum post](http://forum.unity3d.com/threads/unet-sample-projects.331978/):

* Multiplayer 2D Tanks example game
* Multiplayer Invaders game with Matchmaking
* Multiplayer 2D space shooter with Matchmaking
* Minimal Multiplayer project

