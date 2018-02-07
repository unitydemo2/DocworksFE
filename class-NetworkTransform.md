NetworkTransform
====================

The NetworkTransform component synchronizes movement of game objects across the network. This component takes authority into account, so LocalPlayer objects (which have local authority) synchronize their position from the client to server, then out to other clients. Other objects (with server authority) synchronize their position from the server to clients.

To use this component, add it to the prefab or game object that you want to synchronize movement for. The component requires that the game objects has a NetworkIdentity. Note that networked objects must be spawned to synchronize.


Properties
----------

|**_Property:_**|**_Function:_** |
|:---|:---|
|characterContoller	Cached	|  CharacterController.|
|clientMoveCallback2D	| 	A callback that can be used to validate on the server, the movement of client authoritative objects.|
|clientMoveCallback3D	| 	A callback that can be used to validate on the server, the movement of client authoritative objects.|
|grounded	| 	Tells the NetworkTransform that it is on a surface (this is the default).|
|interpolateMovement	| 	Enables interpolation of the synchronized movement.|
|interpolateRotation		| Enables interpolation of the synchronized rotation.|
|lastSyncTime	| 	The most recent time when a movement synchronization packet arrived for this object.|
|movementTheshold	| 	The distance that an object can move without sending a movement synchronization update.|
|rigidbody2D	| 	Cached Rigidbody2D.|
|rigidbody3D	| 	Cached Rigidbody.|
|rotationSyncCompression	| 	How much to compress rotation sync updates.|
|sendInterval	| 	The sendInterval controls how often state updates are sent for this object.|
|snapThreshold	| 	If a movement update puts an object further from its current position than this value, the object snaps to the new position instead of moving smoothly.|
|syncRotationAxis	| 	Which axis should rotation by synchronized for.|
|targetSyncPosition	| 	The target position interpolating towards.|
|targetSyncRotation2D	| 	The target rotation interpolating towards.|
|targetSyncRotation3D	| 	The target position interpolating towards.|
|targetSyncVelocity	| 	The velocity send for synchronization.|
|transformSyncMode	| What method to use to sync the object's position.|


Hints
-----
* There is a NetworkSendRate slider on the inspector of the NetworkTransform. For objects that do not need to update after being created - such as bullet, set this slider to zero.
* The NetworkTransformVisualizer will help NetworkTransform be debugged.



