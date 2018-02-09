NetworkConnection 
==============

NetworkConnection is a HLAPI class that encapsulates a network connection. NetworkClient objects have a NetworkConnections, and NetworkServers have multiple connections - one from each client. NetworkConnections have the ability to send byte arrays, or serialized objects as network messages.

Properties
----------

|**_Property:_** ||**_Function:_** |
|:---|:---|:---|
|__hostId__ ||The NetworkTransport hostId for this connection.|
|__connectionId__ ||The NetworkTransport connectionId for this connection.|
|__isReady__ ||Flag to control whether state updates are sent to this
|__lastMessageTime__ ||The last time that a message was received on this connection.|
|__address__ ||The IP address of the end-point that this connection is connected to. |
|__playerControllers__ ||The set of players that have been added with AddPlayer(). |
|__clientOwnedObjects__ ||The set of objects that this connection has authority over. |

The NetworkConnection class has virtual functions that are called when data is sent to the transport layer or recieved from the transport layer. These functions allow specialized versions of NetworkConnection to inspect or modify this data, or even route it to different sources. These function are show below, including the default behaviour:

````
public virtual void TransportRecieve(byte[] bytes, int numBytes, int channelId)
{
	HandleBytes(bytes, numBytes, channelId);
}

public virtual bool TransportSend(byte[] bytes, int numBytes, int channelId, out byte error)
{
	return NetworkTransport.Send(hostId, connectionId, channelId, bytes, numBytes, out error);
}
````

An example use of these function is to log the contents of incoming and outgoing packets. Below is an example of a DebugConnection class that is derived from NetworkConnection that logs the first 50 bytes of packets to the console. To use a class like this call the SetNetworkConnectionClass() function on a NetworkClient or NetworkServer.

````
class DebugConnection : NetworkConnection
{
	public override void TransportRecieve(byte[] bytes, int numBytes, int channelId)
	{
		StringBuilder msg = new StringBuilder();
		for (int i = 0; i < numBytes; i++)
		{
			var s = String.Format("{0:X2}", bytes[i]);
			msg.Append(s);
			if (i > 50) break;
		}
		UnityEngine.Debug.Log("TransportRecieve h:" + hostId + " con:" + connectionId + " bytes:" + numBytes + " " + msg);

		HandleBytes(bytes, numBytes, channelId);
	}

	public override bool TransportSend(byte[] bytes, int numBytes, int channelId, out byte error)
	{
		StringBuilder msg = new StringBuilder();
		for (int i = 0; i < numBytes; i++)
		{
			var s = String.Format("{0:X2}", bytes[i]);
			msg.Append(s);
			if (i > 50) break;
		}
		UnityEngine.Debug.Log("TransportSend    h:" + hostId + " con:" + connectionId + " bytes:" + numBytes + " " + msg);

		return NetworkTransport.Send(hostId, connectionId, channelId, bytes, numBytes, out error);
	}
}
````
