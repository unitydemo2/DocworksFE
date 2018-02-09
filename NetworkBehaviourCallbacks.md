# NetworkBehaviour callbacks

When using the Network Manager, a player is added by default when a client connects to the server. Players are represented by designated GameObjects (See Unity documentation on [Player GameObjects](UNetPlayers) to learn more). The player GameObject exists on both the __Server__ and the __Client__ instances. 

Different callbacks are received depending on your game’s connection state. These can be set in the Network Manager HUD.

![](../uploads/Main/NetworkManagerHud.png)

Three connection states are available:

* __Host__: To set your game up in __Host__ mode, select __LAN Host(H)__.
* __Client__: To set your game up in __Client__ mode, select __LAN Client(C)__ and enter the server IP into the text field or use the API function `StartClient()`. Note that your server IP must be in the same local network - or you can type "localhost" if you are connecting to the same machine.

* __Server__: To set your game up in __Server__ mode, select __LAN Server Only(S)__.

During run time, the Network Manager HUD’s controls are also available in the Network Manager HUD component’s Inspector window. Click __Runtime Controls__ to access these.

![](../uploads/Main/NetworkManagerHUD2.png)

The callbacks in this section are defined in the [NetworkBehaviour](class-NetworkBehaviour) class and are called only on the player GameObject. To learn more about setting up game states, see [Using the Network Manager: Game state management](http://docs.unity3d.com/Manual/UNetManager.html).

Some callbacks require you to have multiple instances of the game running (for example, two Standalone instances, or one Standalone and one in the Editor). These instances can be on the same machine or on different machines, as long as those machines are connected through a local network. This also works in the same way for MatchMaker, but with MatchMaker your machines can also be connected via the Internet.

#### See also:

* [NetworkBehaviour](class-NetworkBehaviour) 

* [Network Manager callbacks](NetworkManagerCallbacks)

### Player callbacks on Server

To get these callbacks you need to have two instances of the game, one running in __Server__ mode and the other running in __Client__ mode. These callbacks are only called on the player GameObject on the __Server__ instance.

Launch the __Server__ mode instance first, then start the __Client__ instance to get the callbacks:

* `OnStartServer`

* `OnRebuildObservers`

* (`Start()` function is called)

### Player callbacks on Client

To get these callbacks you need to have two instances of the game, one running in __Server__ mode and the other running in __Client__ mode. These callbacks are only called on the player GameObject on the __Client__ instance.

Launch the __Server__ mode instance first, then start the __Client__ instance to get the callbacks:

* `OnStartClient`

* `OnStartLocalPlayer`

* `OnStartAuthority`

* (`Start()` function is called)

### Player callbacks on Host

To get these callbacks you need to have one instance of the game running in __Host__ mode, either in the Editor or as a Standalone build. These callbacks are only called on the Player GameObject:

* `OnStartServer`

* `OnStartClient`

* `OnRebuildObservers`

* `OnStartAuthority`

* `OnStartLocalPlayer`

* (`Start()` function is called)

* `OnSetLocalVisibility`

### NetworkBehaviour: OnNetworkDestroy

To get the `OnNetworkDestroy` callback you need to have three Standalone instances of the game, one running in __Server__ mode and two running in __Client__ mode. 

Follow the instructions below to get the `OnNetworkDestroy` callback:

1. Start __Server__ instance

2. Start __Client__ instance

3. Start a second __Client__ instance

4. When both __Client__ instances have automatically connected to the __Server__ instance, stop one __Client__ instance

5. `OnNetworkDestroy` is then called on the remaining __Client__ instance, but not on the __Server__ instance
