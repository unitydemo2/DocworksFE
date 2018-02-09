Network Lobby Manager
=====================

The NetworkLobbyManager is a specialized type of NetworkManager that provides a multiplayer lobby before entering the main play scene of the game. It allows you to set up a network with:

* A maximum player limit
* Automatic start when all players are ready
* Option to prevent players from joining a game in progress
* Support for "Couch Multiplayer" (i.e. multiple players per client)
* Customizable ways for players to choose options while in lobby

There are two types of player objects with the NetworkLobbyManager:

LobbyPlayer Object

* One for each player
* Created when client connects, or player is added
* Persists until client disconnects
* Holds ready flag and configuration data
* Handles commands in the lobby
* should use the NetworkLobbyPlayer component

GamePlayer Object

* One for each player
* Created when game scene is started
* Destroyed when re-entering lobby
* Handles commands in the game


Properties
----------

|**_Property:_** |**_Function:_** |
|:---|:---|
|__showLobbyGUI__ |Show the developer OnGUI controls for the lobby. |
|__maxPlayers__ |The maximum number of players allowed in the lobby. |
|__maxPlayersPerConnection__ |The maximum number of players allowed to be added for each client connection. |
|__lobbyPlayerPrefab__ |The prefab to create for players when they enter the lobby. |
|__gamePlayerPrefab__ |The prefab to create for players when the game starts. |
|__lobbyScene__ |The scene to use for the lobby. |
|__playScene__ |The scene to use for main game play. |



Details
-------

* The lobbyPlayerPrefab slot should be filled by an object with the NetworkLobbyPlayer component on it.
* There is a GUI for the lobby manager. See the multiplayer-lobby asset package.