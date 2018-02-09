Scene Objects
================

Objects that are created dynamically are added to the network with NetworkServer.Spawn(), but objects that already exist in the scene are handled differently. These objects are loaded with the scene on both the client and server, and exist at runtime before any spawn messages are sent.

All objects in the scene with a NetworkIdentity component will be disabled when the scene is loaded; on both the client and the server. Then, when the scene is fully loaded, NetworkServer.SpawnObjects() is called to activate these networked scene objects. This will be done automatically by the NetworkManager when the server scene finishes loading - or can be called directly by user code. This causes the networked scene objects to be spawned in a special way - the existing instances are hooked up to the network instead of new instances being created.

There are some good reasons to use scene objects instead of dynamically spawned objects. These objects:

 * are loaded with the level, so there will be no pause at runtime
 * can have specific modifications that differ from prefabs
 * can be referenced by other object instances in the scene, which can avoid finding the objects to hook them up at runtime

Once scene objects have been spawned by NetworkServer.SpawnObjects() then they behave like every other spawned objects. Updates will be sent, and ClientRPC calls can be made.

If an object in scene is destroyed on the server before a client joins the game, then it will never be spawned on new clients that join.

Networked scene objects are disabled when the network is started. Any scene object with a NetworkIdentity in the scene is a networked scene object.

On the server, these objects are then enabled when NetworkServer.SpawnObjects() is called - so when the server is started, or when the scene finishes loading on the server. When a client connects, the client is sent a ObjectSpawnScene spawn message for each of the scene objects that exist on the server, that are visible to that client. This messages causes the object on the client to be enabled and has the latest state of that object from the server in it.  So only objects that are visible to the client, and not destroyed on the server, will be activated on the client. And like regular non-scene objects, these scene objects will be started with the latest state when the client joins the game.