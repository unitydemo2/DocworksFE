#Using the Network Manager

The __Network Manager__ is a component for managing the network state of a multiplayer game. It is actually implemented entirely using the [High-level API](UNetUsingHLAPI) (HLAPI), so everything it does is also available to developers through scripting; however, the Network Manager component wraps up a lot of useful functionality into a single place, and makes creating, running and debugging multiplayer games as simple as possible.

The Network Manager can be used entirely without scripting. It has Inspector controls in the Editor that allow configuration of all of its features. The Network Manager HUD supplies a simple, default user interface at run time that allows the networked game to be controlled by the user. For advanced users, developers can derive a class from `NetworkManager` and customize its behaviour by overriding any of the virtual function hooks that it provides.

The Network Manager features include:

* Game state management
* Spawning management
* Scene management
* Debugging information
* Matchmaking
* Customization


##Getting Started with the Network Manager

The Network Manager can be used as the core controlling component of a multiplayer game. To get started, create an empty GameObject in your starting Scene (or pick a convenient GameObject that can host the Network Manager component). Then add the NetworkManager component from the Network/NetworkManager menu item. The newly added NetworkManager component should look something like:

![](../uploads/Main/NetworkManagerInspector.png) 

The Inspector for the Network Manager in the Editor allows you to configure and control many things related to networking.

The Network Manager HUD is another component that works with the Network Manager. It gives you a simple user interface when the game is running to control the network state. This is good for getting started with a network project, but it's not intended to be used as the final UI for a game. The NetworkManagerHUD looks like this:

![](../uploads/Main/NetworkManagerRuntimeUI.png) 

![](../uploads/Main/NetworkManagerMMUI.png) 

Finished games still require a proper user interface for controlling the game state and to allow players to choose what kind of game to play - the Network Manager HUD is intended for development use only.

##Game state management

A Networking multiplayer game can run in three modes - as a client, as a dedicated server, or as a "Host" which is both a client and a server at the same time. Networking is designed to make the same game code and assets work in all of these cases. Developing for the single player version of the game and the multiplayer version of the game should be the same thing.

NetworkManager has functions for entering each of these modes: 

* `NetworkManager.StartClient()`
* `NetworkManager.StartServer()`
* `NetworkManager.StartHost()`

These are all available to script code, so they can be invoked from keyboard input handlers or from custom user interfaces. The default runtime controls that can optionally be displayed also invoke these same functions. There are also buttons in the Network Manager HUD Inspector, available in the Editor in Play Mode, that call the same functions:

![](../uploads/Main/NetworkManagerRuntimeControls.png) 

Whatever function is used to change the game state, the properties `networkAddress` and `networkPort` are used. When a server or host is started, `networkPort` becomes the listen port. When a client is started, `networkAddress` is the address to connect to, and `networkPort` is the port to connect to.

##Spawning management

The Network Manager can be used to manage spawning of networked GameObjects from Prefabs. Most games have a Prefab used as the main player GameObject, so the Network Manager has a slot to drag the player Prefab. When a player Prefab is set, a player GameObject is automatically spawned from that Prefab for each user in the game. This applies to the local player on a hosted server, and remote players on remote clients. Note that the player Prefab must have the Network Identity component on it.

In addition to the player Prefab, the Prefabs of other GameObjects that are dynamically spawned must be registered with the client Scene. This can be done with the `ClientScene.RegisterPrefab()` functions, or it can be done by the Network Manager automatically. Adding Prefabs to the spawn list automatically registers them. The spawn configuration section of the Network Manager inspector looks like this:

![](../uploads/Main/NetworkManagerSpawning.png) 

Once a player Prefab is set, you should be able to start the game as a host and see the player GameObject spawn. Stopping the game should destroy the player GameObject. Running another copy of the game and connecting as a client to localhost should make another player GameObject appear, and stopping that client should make that client's player GameObject be destroyed.

The player GameObject is spawned by the default implementation of `NetworkManager.OnServerAddPlayer`. If you want to customize the way player GameObjects are created, you can override that virtual function. This code shows an example of the default implementation:

````
public virtual void OnServerAddPlayer(NetworkConnection conn, short playerControllerId)
{
	var player = (GameObject)GameObject.Instantiate(playerPrefab, playerSpawnPos, Quaternion.identity);
	NetworkServer.AddPlayerForConnection(conn, player, playerControllerId);
}
````

Note that the function `NetworkServer.AddPlayerForConnection()` must be called for the newly created player GameObject, so that it is spawned and associated with the client's connection. This spawns the GameObject, so `NetworkServer.Spawn` does not need to be called for the player GameObject.

##Start positions

To control where players are spawned, you can use the Network Start Position component. The Network Manager looks for GameObjects in a Scene that have the Network Start Position component attached, and if it finds any, then it spawns the player at the position and orientation of one of them. Use custom code to access the available Network Start Position components by the list `NetworkManager.startPositions`, and a helper function `GetStartPosition()` on the Network Manager that can be used in implementation of `OnServerAddPlayer` to find a start position.

To use start positions, attach a Network Start Position component to a GameObject in the Scene. There can be multiple start positions within a Scene. The Network Manager then registers the position and orientation of the GameObject as a start position. When a client joins the game and a player is added, the player GameObject is created at one of the start positions, with the same position and orientation.

The NetworkManager has a property `PlayerSpawnMethod` which allows configuration of how `startPositions` are chosen. 

* Choose __Random__ to spawn players at randomly chosen `startPosition` options. 
* Choose __Round Robin__ to cycle through `startPosition` options in a set list.

The code for the spawn area looks like this:

````
if (m_PlayerSpawnMethod == PlayerSpawnMethod.Random && s_StartPositions.Count > 0)
{
	// try to spawn at a random start location
	int index = Random.Range(0, s_StartPositions.Count);
	return s_StartPositions[index];
}
if (m_PlayerSpawnMethod == PlayerSpawnMethod.RoundRobin && s_StartPositions.Count > 0)
{
	if (s_StartPositionIndex >= s_StartPositions.Count)
	{
		s_StartPositionIndex = 0;
	}
​
	Transform startPos = s_StartPositions[s_StartPositionIndex];
	s_StartPositionIndex += 1;
	return startPos;
}
````

##Scene management

Most games have more than one Scene. At the very least, there is usually a title screen or starting menu Scene in addition to the Scene where the game is actually played. The Network Manager is set up to automatically manage Scene state and Scene transitions in a way that works for a multiplayer game. There are two slots on the NetworkManager Inspector: the `offlineScene` and the `onlineScene`. Dragging Scene GameObjects into these slots activates networked Scene management. 

When a server or host is started, the online Scene is loaded. This then becomes the current network Scene. Any clients that connect to that server are instructed to also load that Scene. The name of this Scene is stored in the `networkSceneName` property.

When the network is stopped, by stopping the server or host or by a client disconnecting, the offline Scene is loaded. This allows the game to automatically return to a menu Scene when disconnected from a multiplayer game.

You can also change Scenes while the game is active by calling `NetworkManager.ServerChangeScene()`. This makes all the currently connected clients change Scene too, and updates `networkSceneName` so that new clients also load the new Scene.

While networked Scene management is active, any calls to game state management functions such `NetworkManager.StartHost()` or `NetworkManager.StopClient()` can cause Scene changes. This applies to the runtime control UI. By setting up Scenes and calling these functions, it is easy to control the flow of a multiplayer game.

Note that Scene changes cause all the GameObjects in the previous Scene to be destroyed. The Network Manager usually needs to to persist between Scenes (otherwise the network connection is broken upon a Scene change), so ensure the __Don't Destroy On Load__ box is checked in the Inspector. It is also possible to have a Network Manager in each Scene with different settings, which may be helpful if you wish to control incremental Prefab loading, or different Scene transitions.


##Debugging information

The Network Manager HUD Inspector window shows additional information about the state of the network at runtime. This includes:

* Network connections
* Active NetworkIdentity server objects
* Active NetworkIdentity client objects
* Client peers

Registered client message handlers are shown in the Preview window.

![](../uploads/Main/NetworkManagerDebugInfo.png) 


##Matchmaking

The Network Manager runtime UI and Network Manager Inspector UI allow interactions with the matchmaker service. The function `NetworkManager.StartMatchmaker()` enables matchmaking, and populates the `NetworkManager.matchmaker` property with a `NetworkMatch` object. Once this is active, the default UIs use it and callback functions on `NetworkManager` to let you perform simple matchmaking.

There are virtual functions on `NetworkManager` that derived classes can use to customize the behaviour of responding to Matchmaker callbacks.

![](../uploads/Main/NetworkManagerMatchmaker.png) 

##Customization

There are virtual functions on `NetworkManager` that derived classes can use to customize behaviour. When implementing these functions, be sure to take care of the functionality that the default implementations provide. For example, in `OnServerAddPlayer()`, the function `NetworkServer.AddPlayer` must be called to active the player GameObject for the connection.

Functions invoked on the Server/Host:

````
// called when a client connects 
public virtual void OnServerConnect(NetworkConnection conn);

// called when a client disconnects
public virtual void OnServerDisconnect(NetworkConnection conn)
{
	NetworkServer.DestroyPlayersForConnection(conn);
}

// called when a client is ready
public virtual void OnServerReady(NetworkConnection conn)
{
	NetworkServer.SetClientReady(conn);
}

// called when a new player is added for a client
public virtual void OnServerAddPlayer(NetworkConnection conn, short playerControllerId)
{
	var player = (GameObject)GameObject.Instantiate(playerPrefab, playerSpawnPos, Quaternion.identity);
	NetworkServer.AddPlayerForConnection(conn, player, playerControllerId);
}

// called when a player is removed for a client
public virtual void OnServerRemovePlayer(NetworkConnection conn, short playerControllerId)
{
	PlayerController player;
	if (conn.GetPlayer(playerControllerId, out player))
	{
		if (player.NetworkIdentity != null && player.NetworkIdentity.gameObject != null)
			NetworkServer.Destroy(player.NetworkIdentity.gameObject);
	}
}

// called when a network error occurs
public virtual void OnServerError(NetworkConnection conn, int errorCode);
````

Functions invoked on the client:

````
// called when connected to a server
public virtual void OnClientConnect(NetworkConnection conn)
{
	ClientScene.Ready(conn);
	ClientScene.AddPlayer(0);
}

// called when disconnected from a server
public virtual void OnClientDisconnect(NetworkConnection conn)
{
	StopClient();
}

// called when a network error occurs
public virtual void OnClientError(NetworkConnection conn, int errorCode);

// called when told to be not-ready by a server
public virtual void OnClientNotReady(NetworkConnection conn);
````

Functions invoked for the Matchmaker:

````
// called when a match is created
public virtual void OnMatchCreate(CreateMatchResponse matchInfo)

// called when a list of matches is received
public virtual void OnMatchList(ListMatchResponse matchList)

// called when a match is joined
public void OnMatchJoined(JoinMatchResponse matchInfo)
````


