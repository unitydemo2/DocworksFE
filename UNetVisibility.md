Object Visibility
=============================

Unity Networking supports the idea that not all objects on the server should be visible to all players in the game. This is sometimes called "Area of Interest", as players are only given visibility to objects that the game determines are relevant or interesting to them. Some game features that use this concept are Fog Of War, Stealth and proximity based visibility. This is especially important when the game world is very large on the server or contains many networked objects. Reducing the set of objects visible to player reduces login times, and ongoing bandwidth - as updates are only sent to players for objects that are visible to them.

NetworkProximityChecker
-----------------------

The simplest way to restrict object visibility for players is use the built-in [NetworkProximityChecker](class-NetworkProximityChecker) component. This works in conjunction with the Unity 3D physics or 2D physics systems to only allow players to see objects that are close to them. To use this component, add it to the prefab of the networked object that you want to have restricted visibility. The [NetworkProximityChecker](class-NetworkProximityChecker) has some configurable parameters. Objects further away than "Vis Range" will not be visible to a player, and each player's set of visible objects will be recalculated every "Vis Update Interval" seconds.

The object must have a physics collider to work with the [NetworkProximityChecker](class-NetworkProximityChecker). 

Visibility on Remote Clients
----------------------------

When a player on a remote client joins a network game, only objects that are visible to the player will be spawned on that client. So even if the player enters a large world with many networked objects, the time for world entry can be kept reasonable. This applies to networked objects in the scene, but does not affect the loading of assets - the assets for registered prefabs and scene objects are still loaded.

As a player moves within the world, the set of visible objects will change. As this happens, the client is told about these changes. There is an ObjectHide message that is sent to clients when an object is no longer visible. The default behaviour for handling this message is to destroy the object. When an object becomes visible, the client receives an ObjectSpawn message - just as if the object were created for the first time. So by default the object is instantiated like any other spawned object.

Visibility on the Host
----------------------

As the host shares the same scene as the server, it cannot destroy objects that are not visible to the local player. Instead, there is a virtual function on NetworkBehaviour that is invoked:

````
public virtual void OnSetLocalVisibility(bool vis)
{
}
````

This function is invoked on all networked scripts on objects that change visibility state on the host. This allow each script to customize how it should respond, such as by disabling HUD elements or renderers. The default implementation in NetworkProximityChecker disables or enables all Renderer components on the object.


Custom Visibility
-----------------
The NetworkProximityChecker is implemented using the public visibility interface of Unity Networking. Using this interface developers should be able to implement any kind of visibility rules they desire. Each NetworkIdentity keeps track of the set of players that it is visible to. These are called the "observers" of the object.

There is one function on NetworkIdentity:

````
// call this to rebuild the set of players observing this object
public void RebuildObservers(bool initialize);
````

The NetworkProximityChecker calls this function at a fixed interval, so the set of visible objects for each player is updated as they move around.

On the NetworkBehaviour, there are some virtual functions for determining visibility:

````
// called when a new player enters the game
public override bool OnCheckObserver(NetworkConnection newObserver);

// called when RebuildObservers is invoked 
public override bool OnRebuildObservers(HashSet<NetworkConnection> observers, bool initial);
````

The OnCheckObservers function is called on the server on each networked object when a new player enters the game. If it returns true, then that player is added to the object's observers. The NetworkProximityCheck does a simple distance check in its implementation of this function.

The OnRebuildObservers function is called on the server when RebuildObservers is invoked. This function expects the set of observers to be populated with the players that can see the object. The NetworkServer then handles sending ObjectHide and ObjectSpawn messages based on the differences between the old and new visibility sets. The NetworkProximityChecker uses Physics.OverlapSphere() to find the players that are within the visibility distance for this object.

Note that to tell is an object is a player, check if it has a valid "connectionToClient" on its NetworkIdentity. For example:

````
	var hits = Physics.OverlapSphere(transform.position, visRange);
	foreach (var hit in hits)
	{
		// (if an object has a connectionToClient, it is a player)
		var uv = hit.GetComponent<NetworkIdentity>();
		if (uv != null && uv.connectionToClient != null)
		{
			observers.Add(uv.connectionToClient);
		}
	}
````
