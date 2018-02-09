Network Messages
================

In addition to the high level facilities of commands and RPC calls, it is also possible to send raw network messages.

There is a class called MessageBase that can be extended to make serializable network message classes. This class has serialization and deserialization functions that take writer and reader objects. Developers can implement these functions themselves, or rely on code-generated implementations that are automatically created by the networking system. The base class looks like this:

````
public abstract class MessageBase
{
	// De-serialize the contents of the reader into this message
	public virtual void Deserialize(NetworkReader reader) {}

	// Serialize the contents of this message into the writer
	public virtual void Serialize(NetworkWriter writer) {}
}
````

Message classes can contain members that are basic types, structs, arrays, and most of the common Unity Engine types such as Vector3. They cannot contain members that are complex classes or generic containers.

There are built-in message classes for common types of network messages:
 
 * EmptyMessage
 * StringMessage
 * IntegerMessage

To send a message there are Send() functions on the NetworkClient, NetworkServer, and NetworkConnection classes which work the same way. They take a message Id, and a message object that is derived from MessageBase. The code below shows how to send and handle a message using one of the built-in message classes:

````
using UnityEngine;
using UnityEngine.Networking;
using UnityEngine.Networking.NetworkSystem;

public class Begin : NetworkBehaviour
{
	const short MyBeginMsg = 1002;

	NetworkClient m_client;

	public void SendReadyToBeginMessage(int myId)
	{
		var msg = new IntegerMessage(myId);
		m_client.Send(MyBeginMsg, msg);
	}

	public void Init(NetworkClient client)
	{
		m_client = client;
		NetworkServer.RegisterHandler(MyBeginMsg, OnServerReadyToBeginMessage);
	}

	void OnServerReadyToBeginMessage(NetworkMessage netMsg)
	{
		var beginMessage = netMsg.ReadMessage<IntegerMessage>();
		Debug.Log("received OnServerReadyToBeginMessage " + beginMessage.value);
	}
}
````

To declare a custom network message class and use it:

````
using UnityEngine;
using UnityEngine.Networking;

public class Scores : MonoBehaviour
{
	NetworkClient myClient;

	public class MyMsgType {
		public static short Score = MsgType.Highest + 1;
	};

	public class ScoreMessage : MessageBase
	{
		public int score;
		public Vector3 scorePos;
		public int lives;
	}

	public void SendScore(int score, Vector3 scorePos, int lives)
	{
		ScoreMessage msg = new ScoreMessage();
		msg.score = score;
		msg.scorePos = scorePos;
		msg.lives = lives;

		NetworkServer.SendToAll(MyMsgType.Score, msg);
	}

	// Create a client and connect to the server port
	public void SetupClient()
	{
		myClient = new NetworkClient();
		myClient.RegisterHandler(MsgType.Connect, OnConnected);
		myClient.RegisterHandler(MyMsgType.Score, OnScore);
		myClient.Connect("127.0.0.1", 4444);
	}

	public void OnScore(NetworkMessage netMsg)
	{
		ScoreMessage msg = netMsg.ReadMessage<ScoreMessage>();
		Debug.Log("OnScoreMessage " + msg.score);
	}

	public void OnConnected(NetworkMessage netMsg)
	{
		Debug.Log("Connected to server");
	}
}
````

Note that there is no serialization code for the ScoreMessage class in this source code for example. The body of the serialization functions is automatically generated for this class.

Error Message Class
====================
Thre is also a ErrorMessage class that is derived from MessageBase. This class is passed to error callbacks on clients and servers.

The errorCode in the ErrorMessage class corresponds to the Networking.NetworkError enumeration.

````
class MyClient
{
    NetworkClient client;
    
    void Start()
    {
        client = new NetworkClient();
        client.RegisterHandler(MsgType.Error, OnError);
    }
    
    void OnError(NetworkMessage netMsg)
    {
        var errorMsg = netMsg.ReadMessage<ErrorMessage>();
        Debug.Log("Error:" + errorMsg.errorCode);
    }
}
````


