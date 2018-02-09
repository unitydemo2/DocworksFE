Network View
============

(This class is part of the old networking system and is deprecated. See [NetworkIdentity](ScriptRef:Networking.NetworkIdentity.html) for the new networking system).

__Network Views__ are the gateway to creating networked multiplayer games in Unity. They are simple to use, but they are extremely powerful. For this reason, it is recommended that you understand the fundamental concepts behind networking before you start experimenting with Network Views. You can learn and discover the fundamental concepts in the [Network Reference Guide](NetworkReferenceGuide).


![](../uploads/Main/Inspector-NetworkView.png) 

In order to use any networking capabilities, including __State Synchronization__ or __Remote Procedure Calls__, your __GameObject__ must have a Network View attached.


Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__State Synchronization__ |The type of [State Synchronization](net-StateSynchronization) used by this Network View |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Off__ |No State Synchronization will be used. This is the best option if you only want to send [RPCs](net-RPCDetails) |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Reliable Delta Compressed__ |The difference between the last state and the current state will be sent, if nothing has changed nothing will be sent. This mode is ordered. In the case of packet loss, the lost packet is re-sent automatically |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Unreliable__ |The complete state will be sent. This uses more bandwidth, but the impact of packet loss is minimized |
|__Observed__ |The __Component__ data that will be sent across the network |
|__View ID__ |The unique identifier for this Network View. These values are read-only in the Inspector |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Scene ID__ |The number id of the Network View in this particular scene |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Type__ |Either saved to the __Scene__ or __Allocated__ at runtime |


Details
-------


When you add a Network View to a GameObject, you must decide two things


1. What kind of data you want the Network View to send
1. How you want to send that data


###Choosing data to send

The __Observed__ property of the Network View can contain a single Component. This can be a __Transform__, an __Animation__, a __RigidBody__, or a script. Whatever the __Observed__ Component is, data about it will be sent across the network. You can select a Component from the drop-down, or you can drag any Component header directly to the variable. If you are not directly sending data, just using RPC calls, then you can turn off synchronization (no data directly sent) and nothing needs to be set as the Observed property. RPC calls just need a single network view present so you don't need to add a view specifically for RPC if a view is already present.


###How to send the data

You have 2 options to send the data of the __Observed__ Component: __State Synchronization__ and __Remote Procedure Calls__.

To use State Synchronization, set __State Synchronization__ of the Network View to __Reliable Delta Compressed__ or __Unreliable__. The data of the __Observed__ Component will now be sent across the network automatically. 

__Reliable Delta Compressed__ is ordered. Packets are always received in the order they were sent. If a packet is dropped, that packet will be re-sent. All later packets are queued up until the earlier packet is received. Only the difference between the last transmissions values and the current values are sent and nothing is sent if there is no difference.

If it is observing a Script, you must explicitly Serialize data within the script. You do this within the __OnSerializeNetworkView()__ function.

````
using UnityEngine;
using UnityEngine.Network;
using System.Collections;

public class ExampleScript : MonoBehaviour {
	void OnSerializeNetworkView (BitStream stream, NetworkMessageInfo info) {
		float horizontalInput = Input.GetAxis ("Horizontal");
		stream.Serialize (horizontalInput);
	}
}
````
_C# script example_

````
function OnSerializeNetworkView (stream : BitStream, info : NetworkMessageInfo) {
	var horizontalInput : float = Input.GetAxis ("Horizontal");
	stream.Serialize (horizontalInput);
}
````
_JS script example_

The above function always writes (an update from the stream) into horizontalInput, when receiving an update and reads from the variable writing into the stream otherwise. If you want to do different things when receiving updates or sending you can use the __isWriting__ attribute of the BitStream class.

````
using UnityEngine;
using UnityEngine.Network;
using System.Collections;

public class ExampleScript : MonoBehaviour {
	void OnSerializeNetworkView (BitStream stream, NetworkMessageInfo info) {
		float horizontalInput = 0.0;
		if (stream.isWriting) {
			// Sending
			horizontalInput = Input.GetAxis ("Horizontal");
			stream.Serialize (horizontalInput);
		} else {	
			// Receiving
			stream.Serialize (horizontalInput);
			// ... do something meaningful with the received variable
		}
	}
}
````
_C# script example_

````
function OnSerializeNetworkView (stream : BitStream, info : NetworkMessageInfo) {
	var horizontalInput : float = 0.0;
	if (stream.isWriting) {
		// Sending
		horizontalInput = Input.GetAxis ("Horizontal");
		stream.Serialize (horizontalInput);
	} else {
		// Receiving
		stream.Serialize (horizontalInput);
		// ... do something meaningful with the received variable
	}
}
````
_JS script example_

__OnSerializeNetworkView__ is called according to the __sendRate__ specified in the network manager project settings. By default this is 15 times per second.

If you want to use Remote Procedure Calls in your script all you need is a NetworkView component present in the same GameObject the script is attached to. The NetworkView can be used for something else, or in case it's only used for sending RPCs it can have no script observed and state synchronization turned off. The function which is to be callable from the network must have the __@RPC__ attribute. Now, from any script attached to the same GameObject, you call [networkView.RPC()](ScriptRef:NetworkView.RPC.html) to execute the Remote Procedure Call.

````
using UnityEngine;
using UnityEngine.Network;
using System.Collections;

public class ExampleScript : MonoBehaviour {
	GameObject playerBullet;
	NetworkView networkView;

	void Start () {
		networkView = new NetworkView ();
	}

	void Update () {
		if (Input.GetButtonDown ("Fire1")) {
			networkView.RPC ("PlayerFire", RPCMode.All);
		}
	}
	
	[RPC]
	void PlayerFire () {
		Instantiate (playerBullet, playerBullet.transform.position, playerBullet.transform.rotation);
	}
}
````
_C# script example_

````
var playerBullet : GameObject;

function Update () {
	if (Input.GetButtonDown ("Fire1")) {
		networkView.RPC ("PlayerFire", RPCMode.All);
	}
}

@RPC
function PlayerFire () {
	Instantiate (playerBullet, playerBullet.transform.position, playerBullet.transform.rotation);
}
````
_JS script example_

RPCs are transmitted reliably and ordered. For more information about RPCs, see the [RPC Details](net-RPCDetails) page.


Hints
-----



* Read through the [Network Reference Guide](NetworkReferenceGuide) if you're still unclear about how to use Network Views
* State Synchronization does not need to be disabled to use Remote Procedure Calls
* If you have more than one Network View and want to call an RPC on a specific one, use __GetComponents(NetworkView)[i].RPC()__.
