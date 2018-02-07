Network System Concepts
=============================


Server and Host
---------------

In the unity networking system, games have a Server and multiple Clients. When there is no dedicated server, one of the clients plays the role of the server - we call this client the "host".

![](../uploads/Main/NetworkHost.png) 

The host is a server and a client in the same process. The host uses a special kind of client called the LocalClient, while other clients are RemoteClients. The LocalClient communicates with the (local) server through direct function calls and message queues, since it is in the same process. It actually shares the scene with the server. RemoteClients communicate with the server over a regular network connection.

One of the aims of the networking system is for the code for LocalClients and RemoteClients to be the same, so that developers only have to think about one type of client most of the time.

Instantiate and Spawn
---------------------

In Unity, GameObject.Instantiate creates new Unity game objects. But with the networking system, objects must also be "spawned" to be active on the network. This can only be done on the server, and causes the objects to be created on connected clients. Once objects are spawned, the Spawning System uses distributed object life-cycle management and state-synchronization principles.

For more details see  [Spawning](UNetSpawning).


Players, Local Players and Authority
------------------------------------

In the network system, player objects are special. There is a player object associated with each person playing the game, and [command](UNetActions)s are routed to that object. A person cannot invoke a [command](UNetActions) on another person's player object - only their own. So there is a concept of "my" player object. When a player is added and the association is made with a connection, that player object becomes a "local player" object on the client of that player. There is a property isLocalPlayer that is set to true, and a callback OnStartLocalPlayer() that is invoked on the object on the client. The diagram below shows two clients and their local players.

![](../uploads/Main/NetworkLocalPlayers.png) 

Only the player object that is "yours" will have the isLocalPlayer flag set. This can be used to filter input processing, to handle camera attachment, or do any other client side things that should only be done for your player.

In addition to isLocalPlayer, a player object can have "local authority". This means that the player object on its owner's client is responsible for the object - it has authority. This is used most commonly for controlling movement, but can be used for other things also. The  NetworkTransform component understands this and will send movement from the client if this is set. The NetworkIdentity has a checkbox for setting LocalPlayerAuthority.

For non-player objects such as enemies, there is no associated client, so authority resides on the server.

![](../uploads/Main/NetworkAuthority.png) 

There is a property "hasAuthority" on the NetworkBehaviour that can be used to tell if an object has authority. So non-player objects have authority on the server, and player objects with localPlayerAuthority set have authority on their owner's client. 

Client Authority for Non-Player Objects
---------------------------------------

Starting with Unity release 5.2, it is possible to have client authority over non-player objects. There are two ways to do this. One is to spawn the object using [NetworkServer.SpawnWithClientAuthority](ScriptRef:Networking.NetworkServer.SpawnWithClientAuthority) and pass the network connection of the client to take ownership. The other is to use [NetworkIdentity.AssignClientAuthority](ScriptRef:Networking.NetworkIdentity.AssignClientAuthority) with the network connection of the client to take ownership.

Assigning authority to a client causes OnStartAuthority() to be called on NetworkBehaviours on the object, and the property hasAuthority will be true. On other clients the hasAuthority property will still be false. Non-player objects with client authority can send [commands](UNetActions), just like players can. These [commands](UNetActions) are run on the server instance of the object, NOT on the player associated with the connection.

Non-player objects that are to have client authority must have LocalPlayerAuthority checked in their NetworkIdentity.

This example below spawns an object and assigns authority to the client of the player that spawned it.

````
[Command]
void CmdSpawn()
{
	var go = (GameObject)Instantiate(otherPrefab, transform.position + new Vector3(0,1,0), Quaternion.identity);
	NetworkServer.SpawnWithClientAuthority(go, connectionToClient);
}
````


Network Context Properties
---------------------------
There are properties on the NetworkBehaviour class that allow scripts to know what the network context is of a networked object at any time. 

* isServer - true if the object is on a server (or host) and has been spawned.
* isClient - true if the object is on a client, and was created by the server.
* isLocalPlayer - true if the object is a player object for this client.
* hasAuthority - true if the object is owned by the local process

These properties can be seen in the preview window of the object in the Inspector window of the editor.

