Persistence
===========

Persistence is a system for saving [World Anchor](windowsholographic-anchors) states across multiple runs of the same application. This can be thought of as a "save game" functionality for physical locations in the real world. An example of this is remembering where a game board is placed in the world when the application re-launches.

The `WorldAnchorStore` provides basic functionality for saving and loading World Anchors. Retrieve a `WorldAnchorStore` by calling `WorldAnchorStore.GetAsync` and providing it with a callback. Your callback saves the `WorldAnchorStore` returned so that it can be used for future operations.

To save an existing World Anchor, give it a name and call the `Save` function on the `WorldAnchorStore`. See an example below:

````
private void SaveAnchor()
{
	if (!this.savedAnchor) // only save this once
	{
		this.savedAnchor = this.MyWorldAnchorStore.Save("MyAnchor", MyWorldAnchor);
		if (!this.savedAnchor)
		{
			// Anchor failed to save to the store.
			// Handle errors here.
		}
	}
}
````
Loading is essentially a reflection of the above:

````
private void LoadAnchor()
{
	this.savedAnchor = this.Load("MyAnchor", MyWorldAnchor);
	if (!this.savedAnchor)
	{
		// An anchor with that name wasn't saved to the store.  
		// Handle errors here.
	}
}
````

To remove an anchor from the store, call the __Delete__ method on the __WorldAnchorStore__.  To remove all anchors from the store, call the __Clear__ method.

