Player Objects
==============

In the HLAPI of the network system players are special kinds of objects.  They represent the player on the server and so have the ability to run commands (which are secure client-to-server remote procedure calls) from the player's client. In this server authoritative system, other non-player server side objects do not have the capability to receive commands directly from objects on clients. This is both for security and to reduce the complexity of working in a distributed environment. Routing all incoming commands from users through the player object ensures that these messages came from the right place, the right client, and can be handling in a central location. 



When using the NetworkManager, a player is added by default when a client connects to the server. In some situations though, adding players should be deferred until some input event happens, so this behaviour can be turned off with the AutoCreatePlayer checkbox on the NetworkManager. When a player is added, the NetworkManager will instantiate an object from the PlayerPrefab and associate it with the connection. This is actually done by the NetworkManager calling  [NetworkServer.AddPlayerForConnection](ScriptRef:Networking.NetworkServer.AddPlayerForConnection.html). This behaviour can be modified by overriding NetworkManager.OnServerAddPlayer. The default implementation of OnServerAddPlayer instantiates a new player instance from the PlayerPrefab and calls NetworkServer.AddPlayerForConnection to spawn the new player instance. A custom implementation of OnServerAddPlayer must also call NetworkServer.AddPlayerForConnection, but is free to perform any other initialization it requires. The example below customizes the color of a player:

````
class Player : NetworkBehaviour
{
	[SyncVar]
	public Color color;
}

class MyManager : NetworkManager
{
	public override void OnServerAddPlayer(NetworkConnection conn, short playerControllerId)
	{
		GameObject player = (GameObject)Instantiate(playerPrefab, Vector3.Zero, Quaternion.Identity);
		player.GetComponent<Player>().color = Color.Red;
		NetworkServer.AddPlayerForConnection(conn, player, playerControllerId);
	}
}
````

The function NetworkServer.AddPlayerForConnection does not have to be called from within OnServerAddPlayer. As long as the correct connection object and playerControllerId are passed in, it can be called after OnServerAddPlayer has returned. This allows asynchronous steps to happen in between, such as loading player data from a remote data source.

The HLAPI treats players and clients as separate objects. In most cases there is a single player for each client. But, in some situations - such as when there are multiple controllers connected to a console system, they could be multiple player objects for a single connection. When there are multiple players for a connection, the playerControllerId property is used to tell them apart. This is an identifier that is scoped to the connection - so that it literally maps to the id of the controller associated with the player on that client.

The player object passed to [NetworkServer.AddPlayerForConnection](ScriptRef:Networking.NetworkServer.AddPlayerForConnection.html) on the server is automatically spawned by the system, so there is no need to call [NetworkServer.Spawn](ScriptRef:Networking.NetworkServer.Spawn.html) for the player. Once a player is ready, the active [NetworkIdentity](ScriptRef:Networking.NetworkIdentity.html) objects in the scene will be spawned on the player's client. So all networked objects in the game will be created on that client with their latest state, so they are in sync with the other participants of the game.

The playerPrefab on the NetworkManager does not have to be used to create player objects. You could use different methods of creating different players.

The function AddPlayerForConnection does not have to be called from within OnServerAddPlayer. It could be called asynchronously, such as when a request to another service like a database returns information on what kind of player to created.


Ready State
----------------------

In addition to players, client connections also have a "ready" state. A client that is ready is sent spawned objects and state synchronization updates; a client that is not ready, is not sent these updates. When a client initially connects to a server it is not ready. While in this state, the client is able to do things that don't require real-time interactions with the server simulation, such as load scenes, choose avatars or fill out login boxes. Once a client has all their pre-game work done, and all their assets loaded, they can call [ClientScene.Ready](ScriptRef:Networking.ClientScene.Ready.html) to enter the ready state. The simple example above also works, as adding a player with [NetworkServer.AddPlayerForConnection](ScriptRef:Networking.NetworkServer.AddPlayerForConnection.html) also puts the client into the ready state if it is not already in that state.

Clients can send and receive network messages without being ready, which also means without having an active player. So a client at a menu or selection screen can be connected to the game and interact with it, even though they have no player object. There is a section later in this document about sending messages without using commands and RPC calls.

Switching Players
--------------------

The player object for a connection can be replaced with [NetworkServer.ReplacePlayerForConnection](ScriptRef:Networking.NetworkServer.ReplacePlayerForConnection). This can be useful to restrict the commands that can be issued by players at certain times, such as in a pre-game lobby screen.  This function takes the same arguments as AddPlayerForConnection, but allows there to already be a player for that connection. The old player object does not have to be destroyed. The [NetworkLobbyManager](ScriptRef:Networking.NetworkLobbyManager) uses this technique to switch from the LobbyPlayer to a game-play player when all the players in the lobby are ready.

This can also be used to respawn a player after their object is destroyed. In some cases it is better to just disable an object and reset its game attributes on respawn, but to actually replace it with a new object you could use code like:

````
class GameManager
{
    public void PlayerWasKilled(Player player)
    {
        var conn = oldPlayer.connectionToClient;
        var newPlayer = Instantiate<GameObject>(playerPrefab);
        Destroy(oldPlayer.gameObject);
    
        NetworkServer.ReplacePlayerForConnection(conn, newPlayer, 0);
    }
}
````

If the player object for a connection is destroyed, then that client will be unable to execute Commands. They can however still send network messages.

To use ReplacePlayerForConnection you must have the NetworkConnection object for the player's client to establish the relationship between the object and the client. This is usually the property connectionToClient on the [NetworkBehaviour](ScriptRef:Networking.NetworkBehaviour) class, but if the old player has already been destroyed, then that may not be readily available. 

To find the connection, there are some lists available. If using the [NetworkLobbyManager](ScriptRef:Networking.NetworkLobbyManager), then the lobby players are available in [lobbySlots](ScriptRef:Networking.NetworkLobbyManager-lobbySlots). Also, the [NetworkServer](ScriptRef:Networking.NetworkServer) has lists of [connections](ScriptRef:Networking.NetworkServer-connections) and [localConnections](ScriptRef:Networking.NetworkServer-localConnections) . 


