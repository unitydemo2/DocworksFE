# Host Migration

In a multiplayer network game without a dedicated server, one of the peers in the game acts as the center of authority for the game. This peer is called the "host". It runs a server and a “local client”, while the other peers each run a “remote client”.

If the host of a game is lost, then the game cannot continue. The host could be lost because the player left, the host process was killed or crashed, the host’s machine was shut down, or because the network connection of the host was lost.

The “Host Migration” feature allows one of the remote clients to become the new host, so that the multiplayer game can continue.

# How it works

During a multiplayer game with host migration enabled, the addresses of the peers will be distributed to the peers in the game. When the host is lost, one peer can become the new host. The other peers then connect to the new host and the game can continue.

The new NetworkMigrationManager component can be dropped into a multiplayer game that uses the Unity Networking HLAPI, and it allows the game to continue with a new host after the original host is lost. Below is a screenshot of the NetworkMigrationManager in the editor inspector. It shows the current migration state.

![The Network Migration Manager component](../uploads/Main/NetworkMigrationManagerInspector.png)

There is a simple user interface provided by the NetworkMigrationManager, similar to the [NetworkManagerHUD](UNetManager). This user interface is intended for testing and prototyping; a real game would implement a custom user interface for host migration, and probably custom logic - possibly choosing the new host automatically without requiring input from the user.

![The Network Migration Manager prototyping HUD](../uploads/Main/NetworkMigrationManagerHUD.png)

Even though the migration may have occurred because the old host lost connection or quite the game, it is possible for the old host of the game to rejoin the game as a client on the new host.

The state of SyncVars and SyncLists on all networked objects in the scene are maintained during a host migration. This also applies to custom serialized data for objects.

All of the player objects in the game are disabled when the host is lost. Then, when the other clients rejoin the new game on the new host, the corresponding players for those clients are re-enabled on the host, and respawned on the other clients. So no player state data is lost during a host migration.

**NOTE**: Only data that is available to clients will be preserved during a host migration. If there is data that is only on the server, then it will not be available to the client that becomes the new host. So any data on the host that is not stored in SyncVars or SyncLists will not be available after a host migration.

The callback function [OnStartServer](ScriptRef:Networking.NetworkBehaviour.OnStartServer) is invoked for all networked objects when the client becomes a new host.

On the new host, the NetworkMigrationManager uses the function [BecomeNewHost](ScriptRef:Networking.NetworkMigrationManager.BecomeNewHost) to construct a networked server scene from the state in the current ClientScene.

The peers in a game with host migration enabled are identified by their `connectionId` on the server. When a client reconnects to the new host of a game, this connectionId is passed to the new host so that it can match this client with the client that was connected to the old host. This Id is set on the ClientScene as the "reconnectId".

# Non-Player Objects

Non-player objects with client authority are also handled by host migration. The objects owned by each client are disabled and re-enabled the same way that player objects are.

# Identifying Peers 

Before the host is lost, all the peers are connected to the host. They each have a unique connectionId on the host - this is called the "oldConnectionId" in the context of host migration. 

When a new host is chosen and the peers reconnect to it, they supply their "oldConnectionId" to identify which peer they are. This allows the new host to match this reconnecting client to the corresponding player object.

The old host uses a special oldConnectionId of zero to reconnect - since it did not have a connection to the old host, it WAS the old host. There is a constant ClientScene.ReconnectIdHost for this.

When using the built-in user interface, the oldConnectionId is set automatically. It can be set manually using [NetworkMigrationManager.Reset](ScriptRef:Networking.NetworkMigrationManager.Reset) or [ClientScene.SetReconnectId](ScriptRef:Networking.ClientScene.SetReconnectId).


# Host Migration Flow

1. MachineA hosts a game with host-migration enabled
* MachineB starts a client and joins the game with host-migration enabled
    * MachineB is told about peers (MachineA-0, and self (MachineB)-1)
* MachineC starts a client and joins the game with host-migration enabled
    * MachineC is told about peers (MachineA-0, MachineB-1, and self (MachineC)-2)
* MachineA is lost, so the host is lost
* MachineB gets disconnect from host
    1. MachineB callback function is invoked on MigrationManager on client
    * MachineB player objects for all players are disabled
    * MachineB stay in online scene

* MachineB uses utility function to pick the new host, picks self
    1. MachineB calls BecomeNewHost() 
    * MachineB start listening
    * MachineB player object for self is reactivated
    * MachineB The player for MachineB is now back in the game with all its old state

* MachineC gets disconnect from host
    1. MachineC callback function is invoked on MigrationManager on client
    * MachineC player objects for all players are disabled
    * MachineC stay in online scene

* MachineC uses utility function to pick new host, picks MachineB
    * MachineC reconnects to new host

* MachineB receives connection from MachineC
    1. MachineC send reconnect message with oldConnectionId (instead of AddPlayer message)
    * callback function is invoked on MigrationManager on server
    * MachineB uses oldConnectionId to find the disabled player object for that player and re-adds it  with ReconnectPlayerForConnection()
    * player object is re-spawned for MachineC
    * The player for MachineC is now back in the game with all its old state

* MachineA recovers (the old host)
    1. MachineA uses utility function to pick the new host, picks MachineB
    * MachineA “reconnects” to MachineB 

* MachineB receives connection from MachineA

* MachineA send reconnect message with oldConnectionId of zero
    1. callback function is invoked on MigrationManager on server (MachineB)
    * MachineB uses oldConnectionId to find the disabled player object for that player and re-adds it with ReconnectPlayerForConnection()
    * player object is re-spawned for MachineA
    * The player for MachineA is now back in the game with all its old state

	
  
	
# Callback Functions

Callback functions on the NetworkHostMigrationManager

````
// called on client after the connection to host is lost. controls whether to switch scenes
protected virtual void OnClientDisconnectedFromHost(
    NetworkConnection conn, 
    out SceneChangeOption sceneChange)

// called on host after the host is lost. host MUST change scenes
protected virtual void OnServerHostShutdown()

// called on new host (server) when a client from the old host re-connects a player
protected virtual void OnServerReconnectPlayer(
    NetworkConnection newConnection, 
    GameObject oldPlayer, 
    int oldConnectionId, 
    short playerControllerId)

// called on new host (server) when a client from the old host re-connects a player
protected virtual void OnServerReconnectPlayer(
    NetworkConnection newConnection, 
    GameObject oldPlayer, 
    int oldConnectionId, 
    short playerControllerId, 
    NetworkReader extraMessageReader)

// called on new host (server) when a client from the old host re-connects a non-player object
protected virtual void OnServerReconnectObject(
    NetworkConnection newConnection, 
    GameObject oldObject, 
    int oldConnectionId)

// called on both host and client when the set of peers is updated
protected virtual void OnPeersUpdated(
    PeerListMessage peers)

// utility function called by the default UI on client after connection to host was lost, to pick a new host.
public virtual bool FindNewHost(
    out NetworkSystem.PeerInfoMessage newHostInfo, 
    out bool youAreNewHost)

// called when the authority of a non-player object changes
protected virtual void OnAuthorityUpdated(
    GameObject go,
    int connectionId,
    bool authorityState)
````


# Constraints
Data that is only present on the server (the host) will be lost when the host is disconnected. For games to be able to perform host migration correctly, important data must be distributed to the clients, not held secretly on the server.

This works for direct connection games. Additional work is required for this to function with the matchmaker and relay server.
