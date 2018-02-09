Object Spawning
=============================

In Unity, creating new game objects with Instantiate() is sometimes called "spawning". In the network HLAPI the word "spawn" is used to mean something more specific. In the server authoritative model of the network HLAPI, to "spawn" an object on the server means that the object should be created on clients connected to the server, and the object will be managed by the spawning system. Once in the spawning system, state updates are sent to clients when the object changes on the server, and the object will be destroyed on clients when it is destroyed on the server. Spawned objects are also added to the set of networked objects that the server is managing, so that if another client joins the game later, the objects will also be spawned on that client. These objects have a unique network instance Id called "netId" that is the same on the server and clients for each object. This is used to route messages to objects and to identify objects.

When NetworkIdentity objects are spawned on clients, they are created with the current state of the object on the server. This applies to the object's transform, movement state and synchronized variables. So client objects will always be up-to-date when they are created. This avoids issues such as objects being spawned at a wrong initial location, then popping to their correct position when a state update packet arrives.


This sounds great, but there are some immediate questions that this brings up. How is the object created on the clients? And, what if the objects changes in between the time when it is spawned and another client connects? Which version of the object is spawned for the new client then?

Spawning of objects on clients instantiates the client object from the prefab of the object that was passed to [NetworkServer.Spawn](ScriptRef:Networking.NetworkServer.Spawn.html) on the server. The NetworkIdentity inspector preview panel shows the Asset ID of the NetworkIdentity, it is this value that identifies the prefab so that the client can create the objects. For this to work efficiently, there is a registration step that clients have to perform; they must call [ClientScene.RegisterPrefab](ScriptRef:Networking.ClientScene.RegisterPrefab.html) to tell the system about the asset that the client object will be created from. 

Registration of spawn prefabs is most conveniently done by the NetworkManager in the editor. The "Spawn Info" section of the NetworkManager allows you to register prefabs without writing any code. This can also be done through code when a [NetworkClient](ScriptRef:Networking.NetworkClient.html) is created.  To do it in code:

````
using UnityEngine;
using UnityEngine.Networking;

public class MyNetworkManager : MonoBehaviour 
{
	public GameObject alienPrefab;
	
	NetworkClient myClient;

	// Create a client and connect to the server port
	public void SetupClient()
	{
		ClientScene.RegisterPrefab(alienPrefab);

		myClient = new NetworkClient();

		myClient.RegisterHandler(MsgType.Connect, OnConnected);
		myClient.Connect("127.0.0.1", 4444);
	}
}
````

In this example, the user would drag a prefab asset onto the alienPrefab slot on the MyNetworkManager script. So that when a alien object is spawned on the server, the same kind of object will be created on the clients. This registration of assets ensures that the asset is loaded with the scene, so that there is no stall to load the asset when it is created. For more advanced use cases such as object pools or dynamically created assets, there is [ClientScene.RegisterSpawnHandler](ScriptRef:Networking.ClientScene.RegisterSpawnHandler.html) which allows callback functions to be registered for client side spawning. 


Below is a simple example of a spawner that creates a tree with a random number of leaves.

````
class Tree : NetworkBehaviour
{
	[SyncVar]
	public int numLeaves;
}

class MySpawner : NetworkBehaviour
{
    public GameObject treePrefab;

    public void Spawn()
    {
    	GameObject tree = (GameObject)Instantiate(treePrefab, transform.position, transform.rotation);
    	tree.GetComponent<Tree>().numLeaves = Random.Range(10,200);
    	NetworkServer.Spawn(tree);
    }
}

````

To complete this example, the project would have a prefab asset for the tree that has the Tree script and a NetworkIdentity component. Then on the MySpawner instance in the scene, the treePrefab slot would be populated by the tree prefab asset. Also, the tree prefab must be registered as a spawnable object - either using the NetworkManager UI, or using ClientScene.RegisterPrefab() in code.

When this code runs, the tree objects created on clients will have the correct value for numLeaves from the server.


###Constraints

* A NetworkIdentity must be on the root game object of a spawnable prefab
* NetworkBehaviour scripts must be on the same game object as the NetworkIdentity, not on child game objects
* Prefabs can't be registered with the NetworkManager unless they have a NetworkIdentity on their root object

Object Creation Flow
--------------------
The actual flow of operations that takes place for spawning is:

- Prefab with NetworkIdentity component is registered as spawnable
- GameObject is instantiated from the prefab on the server
- Game code sets initial values on the instance (note that 3D physics forces applied here do not take effect immediately)
- NetworkServer.Spawn() is called with the instance
- The state of the SyncVars on the instance on the server are collected by calling OnSerialize() on NetworkBehaviour components
- A network message of type MsgType.ObjectSpawn is sent to connected clients that includes the SyncVar data
- OnStartServer() is called on the instance on the server, and isServer is set to true
- Clients recieve the ObjectSpawn message and create a new instance from the registered prefab
- The SyncVar data is applied to the new instance on the client by calling [OnDeserialize()](ScriptRef:Networking.NetworkBehaviour.OnDeserialize) on NetworkBehaviour components
- OnStartClient() is called on the instance on each client, and isClient is set to true
- As gameplay progresses, changes to SyncVar values are automatically synchronized to clients. This continues until game ends.
- NetworkServer.Destroy() is called on the instance on the server
- A network message of type MsgType ObjectDestroy is sent to clients
- OnNetworkDestroy() is called on the instance on clients, then the instance is destroyed.

Player Objects
--------------
Player objects in the network HLAPI are special in some ways. The flow for spawning player objects with the NetworkManager is:

- Prefab with NetworkIdentity is registered as the PlayerPrefab
- Client connects to the server
- Client calls AddPlayer(), network message of type MsgType.AddPlayer is sent to the server
- Server receives message and calls NetworkManager.OnServerAddPlayer()
- GameObject is instantiated from the PlayerPrefab on the server
- NetworkManager.AddPlayerForConnection() is called with the new player instance on the server
- The player instance is spawned - you do not have to call NetworkServer.Spawn() for the player instance
- A network message of type MsgType.Owner is sent to the client that added the player (only that client!)
- The original client receives the network message
- OnStartLocalPlayer() is called on the player instance on the original client, and isLocalPlayer is set to true

Note that OnStartLocalPlayer() is called after OnStartClient(), as it only happens when the ownership messages arrives from the server after the player object is spawned. So isLocalPlayer will not be set in OnStartClient().

Since OnStartLocalPlayer is only called for YOUR player, it is a good place to perform initialization that should only be done for the local player. This could include enabling input processing, and enabling camera tracking for the player object. Typically only the local player has an active camera.

Spawning Object with Client Authority
------------------------------
It is possible to spawn objects and assign authority of the objects to a particular client. This is done with [NetworkServer.SpawnWithClientAuthority](ScriptRef:Networking.NetworkServer.SpawnWithClientAuthority), which takes the NetworkConnection of the client that will be made the authority as an argument.

For these objects, the property hasAuthority will be true on the client with authority and OnStartAuthority() will be called on the client with authority.  That client will be able to issue commands for that object. On other clients (and on the host), hasAuthority will be false.

Objects spawned with client authority must have LocalPlayerAuthority set in their NetworkIdentity.

For example, to allow a player to spawn and control an object:

````
[Command]
void CmdSpawn()
{
	var go = (GameObject)Instantiate(
	   otherPrefab, 
	   transform.position + new Vector3(0,1,0), 
	   Quaternion.identity);
	   
	NetworkServer.SpawnWithClientAuthority(go, connectionToClient);
}
````


