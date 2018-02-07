#Anchor Sharing

Anchor Sharing is a system for saving a [World Anchor](windowsholographic-anchors) on one device in such a way that it can be loaded onto different devices. 

For example: Two users play a game with a virtual game board placed on a table. For the two users' game boards to line up, both devices require a spatial understanding of where the virtual game board is placed, relative to the real world. Anchor Sharing allows Anchor information to be saved from one user's device and recreated on the other user's device. 

Note that the Anchor Sharing feature does not contain the transport layer necessary to transfer data between devices. Network transport systems provide this functionality. See Unity documentation on [Networking](UNet) for more information on this.

###Exporting Anchors

To export an existing World Anchor, you need a shared name for that Anchor and a `WorldAnchorTransferBatch`. 

The example below shows basic usage of this API. Note that:

1.  You should expect multiple calls to `OnExportDataAvailable`. 
2.  If you set up your application to send data to other devices incrementally, you also need to handle cases where data is sent but the export call fails mid-stream.

````
private void ExportWorldAnchor()
{
	WorldAnchorTransferBatch transferBatch = new WorldAnchorTransferBatch();
	transferBatch.AddWorldAnchor("GameRootAnchor", this.MyWorldAnchor);
	WorldAnchorTransferBatch.ExportAsync(transferBatch, OnExportDataAvailable, OnExportComplete);
}

private void OnExportComplete(SerializationCompletionReason completionReason)
{
	if (completionReason != SerializationCompletionReason.Succeeded)
	{
		// If we have been transferring data and it failed, 
		// tell the client to discard the data
		SendExportFailedToClient();
	}
	else
	{
		// Tell the client that serialization has succeeded.
		// The client can start importing once all the data is received.
		SendExportSucceededToClient();
	}
}

private void OnExportDataAvailable(byte[] data)
{
	// Send the bytes to the client.  Data may also be buffered.
	TransferDataToClient(data); 
}
````

###Importing Anchors

Once the data is received, import it through `WorldAnchorTransferBatch` to then recreate the World Anchor on a different client. 

The example below shows basic usage. Note that importing sometimes fails; if this happens, retry the process.

````
private int retryCount = 10;
private void ImportWorldAnchor(byte[] importedData)
{
	WorldAnchorTransferBatch.ImportAsync(importedData, OnImportComplete);
}
​
private void OnImportComplete(SerializationCompletionReason completionReason, WorldAnchorTransferBatch deserializedTransferBatch)
{
	if (completionReason != SerializationCompletionReason.Succeeded)
	{
		Debug.Log("Failed to import: " + completionReason.ToString());
		if (retryCount > 0)
		{
			retryCount--;
			WorldAnchorTransferBatch.ImportAsync(fileData, OnImportComplete);
		}
		return;
	}
​
	string[] ids = deserializedTransferBatch.GetAllIds();
	foreach (string id in ids)
	{
		GameObject gameObject = GetGameObjectFromAnchorId(id);
		if (gameObject != null)
		{
			transferBatch.LockObject(id, gameObject);
		}
		else
		{
			Debug.Log("Failed to find object for anchor id: " + id);
		}
	}
}
````
