NetworkManager
===============

The NetworkManager is a higher level class that allows you to control the state of a networked game. It provides an interface in the editor to control the configuration of the network, the prefabs used for spawning, and the scenes to use for different network game states.

See [Using the NetworkManager](UNetManager) for more details on these properties.

Properties
----------

|**_Property:_** |**_Function:_** |
|:---|:---|
|__autoCreatePlayer__ |Flag to automatically add a player when a client connects. |
|__channels__ |The number of transport layer QoS Channels. |
|__client__ |The current NetworkClient being used by the manager. |
|__connectionConfig__ |Advanced custom network configuration data. |
|__customConfig__ |Flag to use custom network configuration (advanced). |
|__dontDestroyOnLoad__ |Flag to make the NetworkManager persist between scenes. |
|__globalConfig__ |The transport layer global configuration to be used.|
|__isNetworkActive__ |True if the NetworkServer or NetworkClient is active.|
|__logLevel__ |The level of network logging to write. |
|__matches__ |The list of matches that are available to join.|
|__matchHost__ |Matchmaker host address. |
|__matchInfo__ |A MatchInfo instance that will be used when StartServer() or StartClient() are called.|
|__matchMaker__ |The UMatch matchmaker object.|
|__matchName__ |The name of the current match.|
|__matchPort__ |Matchmaker host port. |
|__matchSize__ |The maximum number of players in the current match.|
|__maxConnections__ |The maximum number of connections allowed by the server. |
|__maxDelay__ |The maximum time in seconds to delay buffered messages. |
|__migrationManager__ |The migration manager being used with the NetworkManager.|
|__networkAddress__ |The network address to connect to. |
|__networkPort__ |The network port used to listen on and connect to. |
|__numPlayers__ |The number of active player objects across all connections on the server.|
|__offlineScene__ |The scene to switch to when the network goes off-line. |
|__onlineScene__ |The scene to switch to when the network goes on-line. |
|__packetLossPercentage__ |The percentage of packet loss to add when network simulator active|
|__playerPrefab__ |The prefab to instantiate for players when a client connects. |
|__playerSpawnMethod__ |Choose __Random__ to spawn players at randomly chosen `startPositions`. Choose __Round Robin__ to cycle through `startPositions` in a set list. |
|__runInBackground__ |Flag to make the player run in the background by default. |
|__scriptCRCCheck__ |Flag for using the script CRC check between server and clients.|
|__secureTunnelEndpoint__ |End point for XBox Live connectivity. |
|__serverBindAddress__ |The IP address to bind the server to.|
|__serverBindToIP__ |Flag to tell the server whether to bind to a specific IP address.|
|__simulatedLatency__ |Latency in milliseconds to add when network simulator active. |
|__spawnPrefabs__ |The set of registered spawnable prefabs. |
|__startPositions__ |The set of NetworkStartPosition objects found in the scene. |
|__useSimulator__ |Flag to use network conditions simulation. |
|__useWebSockets__ |This makes the NetworkServer listen for WebSockets connections instead of normal transport layer connections. |

