NetworkBehaviour 
==============

NetworkBehaviours are special scripts that work with objects with the NetworkIdentity component. These scripts are able to perform HLAPI functions such as Commands, ClientRPCs, SyncEvents and SyncVars.

With the server authoritative system of the Unity Network System, networked objects with NetworkIdentities must be "spawned" by the server using NetworkServer.Spawn(). This causes them to be assigned a NetworkInstanceId and be created on clients that are connected to the server. 

Properties
----------

|**_Property:_** ||**_Function:_** |
|:---|:---|:---|
|__isLocalPlayer__ ||True if this object is the player object for the local client. |
|__isServer__ ||True if this object is running on the server, and has been spawned. |
|__isClient__ ||True if this object is running on a client. |
|__hasAuthority__ ||True if this object is the authoritative version of the object. So either on  the server, or on the client with localPlayerAuthority. |
|__assetId__ ||This is the assetId of the object's NetworkIdentity. |
|__netId__ ||This is the netId of the object's NetworkIdentity. |
|__playerControllerId__ ||This is the playerControllerId of the object's NetworkIdentity. |
|__connectionToServer__ ||NetworkConnection object to use to send to the server. |
|__connectionToClient__ ||NetworkConnection object to use to send to the client. |


NetworkBehaviours have the following features that are described below.

* Synchronized Variables
* Network callbacks
* Server and Client functions
* Sending Commands
* Client RPC Calls
* Networked Events

![](../uploads/Main/UNetDirections.jpg) 

###Synchronized Variables

Member variables of NetworkBehaviours can be synchronized from the server to clients. Since the server is authoritative in this system, synchronization is only in the server-to-client direction. Requests for clients to do things are handled by Commands, not by variables synchronized from clients.

The [SyncVar](ScriptRef:Networking.SyncVarAttribute.html) attribute is used to tag member variables as being synchronized. SyncVars can be any basic type, not classes, lists, or other collections.

````
public class SpaceShip : NetworkBehaviour
{
	[SyncVar]
	public int health;

	[SyncVar]
	public string playerName;
}
````

When the value of a SyncVar is changed on the server, it will be sent to all of the ready clients in the game. When objects are spawned, they are created on the client with the latest state of all SyncVars from the server.

###Network callbacks

There are callback functions that are invoked on NetworkBehaviour script for various network events. These are virtual functions on the base class, so they can be overridden in use code like this:

````
public class SpaceShip : NetworkBehaviour
{
	public override void OnStartServer()
	{
		// disable client stuff
	}

	public override void OnStartClient()
	{
		// register client events, enable effects
	}
}
````

The OnStartServer function is called when an object is spawned on the server, or when the server is started for objects in the scene. The OnStartClient function is called when the object is spawned on the client, or when the client connects to a server for objects in the scene. These functions are useful to do things that are specific to either the client or server, such as suppressing effects on a server, or setting up client-side events.

Note that when a local client is being used, both of these functions will be called on the same object.

Other callbacks include:

* OnSerialize - called to gather state to send from the server to clients
* OnDeSerialize - called to apply state to objects on clients
* OnNetworkDestroy - called on clients when server told the object to be destroyed
* OnStartLocalPlayer - called on clients for player objects for the local client (only)
* OnRebuildObservers - called on the server when the set of observers for an object is rebuild 
* OnSetLocalVisibility - called on a host when the visibility of an object changes for the local client
* OnCheckObserver - called on the server to check visibility state for a new client

###Server and Client functions

Member functions in NetworkBehaviours can be tagged with custom attributes to designate them as server-only or client-only functions. For example:

````
using UnityEngine;
using UnityEngine.Networking;

public class SimpleSpaceShip : NetworkBehaviour
{
	int health;

	[Server]
	public void TakeDamage( int amount)
	{
		// will only work on server
		health -= amount;
	}

	[Client]
	void ShowExplosion()
	{
		// will only run on client
	}

	[ClientCallback]
	void Update()
	{
		// engine invoked callback - will only run on client
	}
}
````

These attributes make the function return immediately if they are called when the client or server is not active. They do not generate compile time errors, but they will emit a warning log message if called in the wrong scope. The attributes [ServerCallback](ScriptRef:Networking.ServerCallbackAttribute.html) and [ClientCallback](ScriptRef:Networking.ClientCallbackAttribute.html) can be used for engine callback functions that user code does not control the calling of. These attributes do not cause a warning to be generated.

###Sending Commands

Commands are the way for clients to request to do something on the server. Since the HLAPI is a server authoritative system, clients can ONLY do things through commands. Commands are run on the player object on the server that corresponds to the client that sent the command. This routing happens automatically, so it is impossible for a client to send a command for a different player.

Commands must begin with the prefix "Cmd" and have the [Command] custom attribute on them, like below:

````
using UnityEngine;
using UnityEngine.Networking;

public class SpaceShip : NetworkBehaviour
{
	bool alive;
	float thrusting;
	int spin;

	[Command]
	public void CmdThrust(float thrusting, int spin)
	{	
		if (!alive)
		{
			this.thrusting = 0;
			this.spin = 0;
			return;
		}
			
		this.thrusting = thrusting;
		this.spin = spin;
	}

	[ClientCallback]
	void Update()
	{
		int spin = 0;
		if (Input.GetKey(KeyCode.LeftArrow))
		{
			spin += 1;
		}
		if (Input.GetKey(KeyCode.RightArrow))
		{
			spin -= 1;
		}
		// this will be called on the server
		CmdThrust(Input.GetAxis("Vertical"), spin);
	}
}
````

Commands are called just by invoking the function normally on the client. But instead of the command function running on the client, it will be invoked on the player object of that client on the server. So, commands are typesafe, have built-in security and routing to the player, and use an efficient serialization mechanism for the arguments to make calling them fast.

###Client RPC Calls

Client RPC calls are a way for server objects to cause things to happen on client objects. This is the reverse direction to how commands send messages, but the concepts are the same. Client RPC calls however are not only invoked on player objects, they can be invoked on any NetworkIdentity object. They must begin with the prefix "Rpc" and have the [ClientRPC] custom attribute, like below:

````
using UnityEngine;
using UnityEngine.Networking;

public class SpaceShipRpc : NetworkBehaviour
{
	[ClientRpc]
	public void RpcDoOnClient(int foo)
	{
		Debug.Log("OnClient " + foo);
	}

	[ServerCallback]
	void Update()
	{
		int value = UnityEngine.Random.Range(0,100);
		if (value < 10)
		{
			// this will be invoked on all clients
			RpcDoOnClient(value);
		}
	}
}
````

###Networked Events

Networked events are like Client RPC calls, but instead of just calling a function on the client object, an Event on the client object is triggered. Other scripts that are registered for the event are then invoked - with the arguments from the server, so this allows networked inter-script interactions on the client. Events must start with the prefix "Event" and have the [SyncEvent](ScriptRef:Networking.SyncEventAttribute.html) custom attribute.

Events can be used to build powerful networked game systems that can be extended by other scripts. This example shows how an effect script on the client can respond to events generated by a combat script on the server.

````
using UnityEngine;
using UnityEngine.Networking;

// Server script
public class MyCombat : NetworkBehaviour
{
	public delegate void TakeDamageDelegate(int amount);
	public delegate void DieDelegate();
	public delegate void RespawnDelegate();
	
	float deathTimer;
	bool alive;
	int health;

	[SyncEvent(channel=1)]
	public event TakeDamageDelegate EventTakeDamage;
	
	[SyncEvent]
	public event DieDelegate EventDie;
	
	[SyncEvent]
	public event RespawnDelegate EventRespawn;

	[Server]
	void EventTakeDamage(int amount)
	{
		if (!alive)
			return;
			
		if (health > amount) {
			health -= amount;
		}
		else
		{
			health = 0;
			alive = false;
			// send die event to all clients
			EventDie();
			deathTimer = Time.time + 5.0f;
		}
	}

	[ServerCallback]
	void Update()
	{
		if (!alive)
		{
			if (Time.time > deathTimer)
			{
				Respawn();
			}
			return;
		}
	}

	[Server]
	void Respawn()
	{
		alive = true;
		// send respawn event to all clients
		EventRespawn();
	}
}
````

Hints
-----
* This is a base class that provides Commands and ClientRpc calls.
