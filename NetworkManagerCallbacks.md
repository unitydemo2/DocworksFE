# Network Manager callbacks

This section covers the Network Manager callbacks received depending on the type of connection you have to your game’s Host server.

See documentation on [NetworkBehaviour callbacks](NetworkBehaviourCallbacks) for more information on networking callbacks.

## Local connection callbacks

Different callbacks are received depending on your game’s state. Three states are available. These can be set in the [Network Manager HUD](class-NetworkManagerHUD).

![](../uploads/Main/LocalConnectionCallBack.png)


* __Host__: To set your game up in __Host__ mode, select __LAN Host(H)__ or use the API function `StartHost()`.

* __Client__: To set your game up in __Client__ mode, select __LAN Client(C)__ and enter the server IP into the text field, or use the API function `StartClient()`. Note that your server IP must be in the same local network - or you can type "localhost" if you are connecting to the same machine.

* __Server__: To set your game up in __Server__ mode, select __LAN Server Only(S)__ or use the API function `StartServer()`.

During run time, the Network Manager HUD’s controls are also available in the Network Manager HUD component’s Inspector window. Click __Runtime Controls__ to access these.


![](../uploads/Main/NetworkManagerHUD2.png)


This page details the callbacks received for each mode. To learn more about setting up game states, see [Using the Network Manager: Game state management](http://docs.unity3d.com/Manual/UNetManager.html).

Some Network Manager callbacks require you to have multiple instances of the game running (for example, two Standalone instances, or one Standalone and one in the Editor). These instances can be on the same machine or on different machines, as long as those machines are connected through a local network.

### Host callbacks

To get these callbacks you need to have two instances of the game, one running in __Host__ mode and the other running in __Client__ mode. These callbacks are only called on instances that are running in __Host__ mode.

Follow the steps below to get the callbacks. To stop an instance, press __Stop__ or use the API function `StopHost()`.

Step 1: Start __Host__ instance

* (`Start()` function is called)

* `OnStartHost`

* `OnStartServer`

* `OnServerConnect`

* `OnStartClient`

* `OnClientConnect`

* `OnServerSceneChanged`

* `OnServerReady`

* `OnServerAddPlayer`

* `OnClientSceneChanged`

Step 2: Start __Client__ instance

* `OnServerConnect`

* `OnServerReady`

* `OnServerAddPlayer`

Step 3: Stop __Client__ instance

* `OnServerDisconnect`

Step 4: Stop __Host__ instance

* `OnStopHost`

* `OnStopServer`

* `OnStopClient`

### Client callbacks

To get these callbacks you need to have two instances of the game, one running in __Server__ mode and the other running in __Client__ mode. These callbacks are only called on instances that are running in __Client__ mode.

Launch the __Server__ mode instance first, then follow the steps below to get the callbacks. To stop an instance, press __Stop__ or use the API function `StopHost()`

Step 1: Start __Client__ instance 

* (`Start()` function is called)

* `OnStartClient`

* `OnClientConnect`

* `OnClientSceneChanged`

Step 2: Stop **Server** instance 

* `OnStopClient`

* `OnClientDisconnect`

### Server callbacks

To get these callbacks you need to have two instances of the game, one running in __Server__ mode and the other running in __Client__ mode. These callbacks are only called on instances that are running in __Server__ mode.

Follow the steps below to get the callbacks. To stop an instance, press __Stop__ or use the API function `StopHost()`.

Step 1: Start __Server__ instance 

* (Start() function is called)

* `OnStartServer`

* `OnServerSceneChanged`

Step 2: Start __Client__ instance 

* `OnServerConnect`

* `OnServerReady`

* `OnServerAddPlayer`

Step 3: Stop __Client__ instance

* `OnServerDisconnect`

Step 4: Stop __Server__ instance 

* `OnStopServer`

## Internet connection callbacks

Internet connections to the Host server take place through the Unity MatchMaker system, which connects you via a relay server.

Different callbacks are received depending on your game’s state. Two states are available for MatchMaker: __Host__ and __Client__. To use MatchMaker, run the game and select __Enable Match Maker (M)__ from the Network Manager HUD menu:

![](../uploads/Main/EnableMatchMaker.png)

This opens the MatchMaker menu:

![](../uploads/Main/MatchMakerMenu.png)

* __Host__: To set your game up in __Host__ Mode, select __Enable Match Maker (M)__ > __Create Internet Match__ or use the API function `CreateMatch()`

* __Client__: To set your game up in __Client__ mode, select __Enable Match Maker (M)__ > __Find Internet Match__ > __Join Internet Match__ or use the API function `JoinMatch()`

This page details the callbacks received for each mode. To learn more about setting up game states, see [Using the Network Manager: Game state management](http://docs.unity3d.com/Manual/UNetManager.html).

Some Network Manager callbacks require you to have multiple instances of the game running (for example, two Standalone instances, or one Standalone and one in the Editor). These instances can be on the same machine or on different machines, and on the same network or different networks, but all machines must have an Internet connection. MatchMaker allows you to connect instances of your game via the Internet, so machines with instances of your game could be situated in different parts of the world.

### Host MatchMaker callbacks

To get these callbacks you need to have two instances of the game, one running in __Host__ mode and the other running in __Client__ mode. These callbacks are only called on instances that are running in __Host__ mode.

Follow the steps below to get the callbacks. To stop an instance, press __Stop__ or use the API function `StopHost()`.

Step 1: Start __Host__ instance 

* (`Start()` function is called)

* `OnStartHost`

* `OnStartServer`

* `OnServerConnect`

* `OnStartClient`

* `OnMatchCreate`

* `OnClientConnect`

* `OnServerSceneChanged`

* `OnServerReady`

* `OnServerAddPlayer`

* `OnClientSceneChanged`

Step 2: Start __Client__ instance and select __Join Internet Match__ or use the API function `JoinMatch()`

* `OnServerConnect`

* `OnServerReady`

* `OnServerAddPlayer`

Step 3: Stop __Client__ instance 

* `OnServerDisconnect`

### Client MatchMaker callbacks

To get these callbacks you need to have two instances of the game running, one in __Host__ mode and the other running in __Client__ mode. These callbacks are only called on instances that are running in __Client__ mode.


Launch the __Host__ mode instance first, then the __Client__ instance. Follow the steps below to get the callbacks. To stop an instance, press __Stop__ or use the API function `StopHost()`.

Step 1: On the __Client__ instance, press __Find Internet Match__ or use the API function `ListMatches()` to find a list of online games

* (`Start()` function is called)

* `OnMatchList`

Step 2: On the __Client__ instance, press __Join Match__ or use the API function `JoinMatch()` to join an online game 

* `OnStartClient`

* `OnMatchJoined`

* `OnClientConnect`

* `OnClientSceneChanged`

Step 3: Stop __Host__ instance

* `OnStopClient`

* `OnClientDisconnect`