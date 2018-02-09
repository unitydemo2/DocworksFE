NetworkWriter 
==============

NetworkWriter is a High Level API class for writing objects to byte streams. This class works in conjunction with NetworkReader. NetworkWriter has specific serialization functions for many Unity types.

The NetworkWriter can be used with the MessageBase class to make byte arrays that contain serialized network messages.

````
void SendMessage(short msgType, MessageBase msg, int channelId)
{
	// write the message to a local buffer
	NetworkWriter writer = new NetworkWriter();
	writer.StartMessage(msgType);
	msg.Serialize(writer);
	writer.FinishMessage();

	myClient.SendWriter(writer, channelId);
}
````

This message will be correctly formated so that a message handler function can be invoked for it.
