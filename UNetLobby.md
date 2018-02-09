# Multiplayer Lobby

Many multiplayer games have a staging area (often known as a "lobby") for players to join before playing the actual game. In this area, players can pick options and set themselves as ready for the game to start.

The [NetworkLobbyManager](ScriptRef:Networking.NetworkLobbyManager.html) is a specialized [NetworkManager](ScriptRef:Networking.NetworkManager.html) that provides a lobby for Unity Multiplayer games. Its functionality includes the following:

* Limits the number of players that can join
* Supports multiple players per client, with a limit on the number of players per client
* Prevents players from joining game in-progress
* Has a per-player ready state, so that the game starts when all players are ready
* Has per-player configuration data
* Allows re-joining the lobby when the game is finished
* Virtual functions that allow custom logic for lobby events
* A simple user interface for interacting with the lobby

Below are the NetworkLobbyManager virtual functions called on the server:

* [OnLobbyStartHost](ScriptRef:Networking.NetworkLobbyManager.OnLobbyStartHost)
* [OnLobbyStopHost](ScriptRef:Networking.NetworkLobbyManager.OnLobbyStopHost)
* [OnLobbyStartServer](ScriptRef:Networking.NetworkLobbyManager.OnLobbyStartServer)
* [OnLobbyServerConnect](ScriptRef:Networking.NetworkLobbyManager.OnLobbyServerConnect)
* [OnLobbyServerDisconnect](ScriptRef:Networking.NetworkLobbyManager.OnLobbyServerDisconnect)
* [OnLobbyServerSceneChanged](ScriptRef:Networking.NetworkLobbyManager.OnLobbyServerSceneChanged)
* [OnLobbyServerCreateLobbyPlayer](ScriptRef:Networking.NetworkLobbyManager.OnLobbyServerCreateLobbyPlayer)
* [OnLobbyServerCreateGamePlayer](ScriptRef:Networking.NetworkLobbyManager.OnLobbyServerCreateGamePlayer)
* [OnLobbyServerPlayerRemoved](ScriptRef:Networking.NetworkLobbyManager.OnLobbyServerPlayerRemoved)
* [OnLobbyServerSceneLoadedForPlayer](ScriptRef:Networking.NetworkLobbyManager.OnLobbyServerSceneLoadedForPlayer)
* [OnLobbyServerPlayersReady](ScriptRef:Networking.NetworkLobbyManager.OnLobbyServerPlayersReady)

All of the above server functions have empty default implementations, except for `OnLobbyServerPlayersReady`, which calls `ServerChangeScene` with the PlayScene.

Below are the NetworkLobbyManager virtual functions called on the client:

* [OnLobbyClientEnter](ScriptRef:Networking.NetworkLobbyManager.OnLobbyClientEnter)
* [OnLobbyClientExit](ScriptRef:Networking.NetworkLobbyManager.OnLobbyClientExit)
* [OnLobbyClientConnect](ScriptRef:Networking.NetworkLobbyManager.OnLobbyClientConnect)
* [OnLobbyClientDisconnect](ScriptRef:Networking.NetworkLobbyManager.OnLobbyClientDisconnect)
* [OnLobbyStartClient](ScriptRef:Networking.NetworkLobbyManager.OnLobbyStartClient)
* [OnLobbyStopClient](ScriptRef:Networking.NetworkLobbyManager.OnLobbyStopClient)
* [OnLobbyClientSceneChanged](ScriptRef:Networking.NetworkLobbyManager.OnLobbyClientSceneChanged)
* [OnLobbyClientAddPlayerFailed](ScriptRef:Networking.NetworkLobbyManager.OnLobbyClientAddPlayerFailed)
 
All of the above client functions have empty default implementations.

## Lobby player objects

There are two kinds of player objects, each of which has a Prefab slot in the NetworkLobbyManager. The slots can be seen in this screenshot:

![](../uploads/Main/NetworkLobbyManager.png) 

The LobbyPlayer is created from the LobbyPlayerPrefab when a player joins the lobby:

* One LobbyPlayer for each player
* Created when client connects, or player is added
* Exists until client disconnects
* Holds the ready flag for this player for the lobby
* Handles commands while in the lobby
* Add user scripts to this prefab to hold game-specific player data
* This prefab must have a [NetworkLobbyPlayer](ScriptRef:Networking.NetworkLobbyPlayer) component

### Minimum Players

The __Minimum Players__ field represents the minimum number of "Ready" players in the Lobby to start the Match with. If the number of connected clients is more than the "Minimum Players" value, then waiting for all connected clients to become "Ready" starts the Match.

For example if "Minimum Players" is set to 2:

- Start one instance of the game and start Host. Then in game Lobby UI press __Start__ for your player. You are still in Lobby mode, because the minimum number of Ready players to start the game is 2.
- Start two more instances of the game, and start Clients there. It doesn't matter that "Minimum Players" set to 2. Wait for all connected players to become Ready.
- Press __Start__ in Lobby UI for one player. Two players are Ready, but still in Lobby mode. Press "Start" in the Lobby UI for the last player, and all players are moved to Game mode.

###GamePlayer

The GamePlayer is created from the GamePlayerPrefab when the game starts:

* One GamePlayer for each player
* Created when game Scene is started
* Destroyed when re-entering lobby
* Handles commands while in the game
* This Prefab must have a [NetworkIdentity](ScriptRef:Networking.NetworkIdentity) component

The [NetworkLobbyPlayer](ScriptRef:Networking.NetworkLobbyPlayer.html) component is used for LobbyPlayer objects. It supplies some virtual function callbacks that can be used for custom lobby behaviour

````
	public virtual void OnClientEnterLobby();
	public virtual void OnClientExitLobby();
	public virtual void OnClientReady(bool readyState);
````

The function [OnClientEnterLobby](ScriptRef:Networking.NetworkLobbyPlayer.OnClientEnterLobby) is called on the client when the game enters the lobby. This happens when the lobby Scene starts for the first time, and also when returning to the lobby from the gameplay Scene.

The function [OnClientExitLobby](ScriptRef:Networking.NetworkLobbyPlayer.OnClientExitLobby) is called on the client when the game exits the lobby. This happens when switching to the gameplay Scene.

The function [OnClientReady](ScriptRef:Networking.NetworkLobbyPlayer.OnClientReady) is called on the client when the ready state of that player changes.


##Adding the lobby to a game

Process for adding a NetworkLobby to a multiplayer game (without using the multiplayer-lobby asset package):

* Create a new lobby Scene
* Add the Scene to the Build Settings (menu: __File__ > __Build Settings...__), as the first Scene
* Create a new GameObject in the new Scene (menu: __GameObject__ > __Create Empty__), and name it _LobbyManager_
* Add the NetworkLobbyManager component to the _LobbyManager_ GameObject
* Add the NetworkManagerHUD component to the LobbyManager GameObject
* In the Inspector window for the NetworkLobbyManager component, set the __Lobby Scene__ slot of the NetworkLobbyManger to the Scene that contains the _LobbyManager_ GameObject
* Set the __Play Scene__ slot of the NetworkLobbyManager to the main gameplay Scene for the game
* Create a new GameObject and name it _LobbyPlayer_
* Add the NetworkLobbyPlayer component to the _LobbyPlayer_
* Create a Prefab for the LobbyPlayer (drag it into the Project window), and delete the instance from the Scene
* On the _LobbyManager_'s NetworkLobbymanager component, assign the _LobbyPlayer_ prefab to the __Lobby Player Prefab__ slot
* Assign the Prefab for the player in the main game to the __Game Player Prefab__ slot
* Save the Scene
* Run the game

This version of the NetworkLobbyManager uses the OnGUI user interface like the [NetworkManagerHUD](ScriptRef:Networking.NetworkManagerHUD.html). For a better user interface, use the multiplayer-lobby Asset package (found in the [NetworkStarter sample package](https://forum.unity3d.com/threads/unet-sample-projects.331978/), on the Unity forums).

The NetworkLobbyManager has many virtual function callbacks that can be used for custom lobby behaviour. The most important is [OnLobbyServerSceneLoadedForPlayer](ScriptRef:Networking.NetworkLobbyManager.OnLobbyServerSceneLoadedForPlayer), which is called on the server for each player as they transition from the lobby to the main game. This is the ideal place to apply settings from the lobby to the player object.

````
	// for users to apply settings from their lobby player object to their in-game player object
	
	public override bool OnLobbyServerSceneLoadedForPlayer(GameObject lobbyPlayer, GameObject gamePlayer)
	{
		var cc = lobbyPlayer.GetComponent<ColorControl>();
		var player = gamePlayer.GetComponent<Player>();
		player.myColor = cc.myColor;
		return true;
	}
````

## Sample project

There is a sample project on the Unity asset store that uses the NetworkLobbyManager and provides a GUI for the lobby. This can be used as a starting point for making a multiplayer game with a lobby.

[Lobby Sample Project](https://www.assetstore.unity3d.com/en/#!/content/41836)


