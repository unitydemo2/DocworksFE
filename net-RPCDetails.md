RPC Details (Legacy)
============================

*(For new projects, you should use the [new networking system introduced in 5.1](UNet.html). This information is for legacy projects using the old networking system.)*

__Remote Procedure Calls__ (RPCs) let you call functions on a remote machine. Invoking an RPC is similar to calling a normal function and almost as easy but there are some important differences to understand.


1. An RPC call can have as many parameters as you like but the network bandwidth involved will increase with the number and size of parameters. You should keep parameters to a minimum in order to get the best performance.


1. Unlike a normal function call, an RPC needs an additional parameter to denote the recipients of the RPC request. There are several possible RPC call modes to cover all common use cases. For example, you can easily invoke the RPC function on all connected machines, on the server alone, on all clients but the one sending the RPC call or on a specific client.

RPC calls are usually used to execute some event on all clients in the game or pass event information specifically between two parties, but you can be creative and use them however you like. For example, a server for a game which only starts after four clients have connected could send an RPC call to all clients as soon as the fourth one connects, thus starting the game. A client of a particular player could send RPC calls to everyone to signal that they picked up an item. A server could send an RPC to a particular client to initialize the player right after they connect, for example, to assign them their player number, spawn location, team color, etc. A client could in turn send an RPC only to the server to specify starting options, such as the color they prefer or the items they have bought.


Using RPCs
----------


A function must be marked as an RPC before it can be invoked remotely. This is done by prefixing the function in the script with an RPC attribute:

````
using UnityEngine;
using System.Collections;

public class ExampleScript : MonoBehaviour {
	[RPC]
	void PrintText (string text)
	{
		Debug.Log(text);
	}
}
````
_C# script example_

````
// All RPC calls need the @RPC attribute!
@RPC
function PrintText (text : String)
{
    Debug.Log(text);
}
````
_JS script example_

All network communication is handled by NetworkView components, so you must attach one to the object whose script declares the RPC functions before they can be called.


Parameters
----------


You can use the following variable types as parameters to RPCs:-


* int
* float
* string
* NetworkPlayer
* NetworkViewID
* Vector3
* Quaternion

For example, the following code invokes an RPC function with a single string parameter:

````
using UnityEngine;
using UnityEngine.Network;
using System.Collections;

public class ExampleScript : MonoBehaviour {
	NetworkView networkView;

	void Start() {
		networkView = new NetworkView ();
		networkView.RPC ("PrintText", RPCMode.All, "Hello world");
	}
}
````
_C# script example_

````
networkView.RPC ("PrintText", RPCMode.All, "Hello world");
````
_JS script example_

The first parameter of __RPC()__ is the name of the function to be invoked while the second determines the targets on which it will be invoked. In this case we invoke the RPC call on everyone who is connected to the server (but the call will not be buffered to wait for clients who connect later - see below for further details about buffering).

All parameters after the first two are the ones that will be passed to the RPC function and be sent across the network. In this case, "Hello World" will be sent as a parameter and be passed as the text parameter in the PrintText function.

You can also access an extra internal parameter, a [NetworkMessageInfo](ScriptRef:NetworkMessageInfo.html) struct which holds additional information, such as where the RPC call came from. This information will be passed automatically, so the PrintText function shown above will be can be declared as:

````
using UnityEngine;
using System.Collections;

public class ExampleScript : MonoBehaviour {
	[RPC]
	void PrintText (string text, NetworkMessageInfo info)
	{
		Debug.Log(text + " from " + info.sender);
	}
}
````
_C# script example_

````
@RPC
function PrintText (text : String, info : NetworkMessageInfo)
{
    Debug.Log(text + " from " + info.sender);
}
````
_JS script example_

...while being invoked the same way as before.

As mentioned above, a Network View must be attached to any GameObject which has a script containing RPC functions. If you are using RPCs exclusively (ie, without state synchronisation) then the Network View's __State Synchronization__ can be set to __Off__.


RPC Buffer
----------


RPC calls can also be buffered. Buffered RPC calls are stored up and executed in the order they were issued for each new client that connects. This can be a useful way to ensure that a latecoming player gets all necessary information to start. A common scenario is that every player who joins a game should first load a specific level. You could send the details of this level to all connected players but also buffer it for any who join in the future. By doing this, you ensure that the new player receives the level information just as if they had been present from the start.

You can also remove calls from the RPC buffer when necessary. Continuing the example above, the game may have moved on from the starting level by the time a new player joins, so you could remove the original buffered RPC and send a new one to request the new level.
