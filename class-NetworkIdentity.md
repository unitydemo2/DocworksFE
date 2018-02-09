NetworkIdentity
===============

The NetworkIdentity component is a Unity component that is at the heart of the new networking system. It can be added to objects from the AddComponents->Network->NetworkIdentity menu item. This component controls an object's network identity, and it makes the networking system aware of it. This shows what the NetworkIdentity component looks like on an object:

![](../uploads/Main/NetworkIdentityScreenshot.png) 

With the server authoritative system of the Unity Network System, networked objects with NetworkIdentities must be "spawned" by the server using NetworkServer.Spawn(). This causes them to be assigned a NetworkInstanceId and be created on clients that are connected to the server. 

Scene objects are treated a bit differently than dynamically instantiated objects. These objects are all present in the scene on both client and server. However, when building the game all the scene objects with network identities are disabled. When the client connects to the server the server tells the client which scene objects should be enabled and what their most up to date state information is through spawn messages. This ensures the client will not contain objects placed at now incorrect locations when they start playing, or even objects which will be deleted immediately on connection because some event removed them before the client connected. The **Server Only** checkbox will ensure this a particular object will not be spawned or enabled on clients. 

The **local player authority** setting allows this object to be controlled by the client that owns it - the local player object on that client has authority over it. This is used by other components such as NetworkTransform.

This component contains tracking information like what scene ID, network ID and asset ID the object has been assigned. The scene ID is valid in all scene objects with a NetworkIdentity component. The network ID is the ID of this particular object instance, there might be multiple objects instantiated of a particular object type and the network ID is used to identity which object, for example, a network update should be applied to. The asset ID refers to what source asset the object was instantiated from. This is used internally when an particular object prefab is spawned over the network. This information is exposed in the preview panel at the bottom of the inspector:

![](../uploads/Main/NetworkIdentityPreview.png)

At runtime there is more information to display here (a disabled NetworkBehaviour is displayed non-bold):

![](../uploads/Main/NetworkIdentityPreviewRuntime.png)


Properties
----------

|**_Property:_** |**_Function:_** |
|:---|:---|
|__assetId__ |This identifies the prefab associated with this object (for spawning). |
|__clientAuthorityOwner__ |The client that has authority for this object. This will be null if no client has authority. |
|__connectionToClient__ |The connection associated with this NetworkIdentity. This is only valid for player objects on the server. |
|__connectionToServer__ |The UConnection associated with this NetworkIdentity. This is only valid for player objects on a local client. |
|__hasAuthority__ |True if this object is the authoritative version of the object. So either on a the server, or on the client with localPlayerAuthority. |
|__isClient__ |True if this object is running on a client. |
|__isLocalPlayer__ |This returns true if this object is the one that represents the player on the local machine. |
|__isServer__ |True if this object is running on the server, and has been spawned. |
|__localPlayerAuthority__ |True if this object is controlled by the client that owns it - the local player object on that client has authority over it. This is used by other components such as NetworkTransform. |
|__netId__ |A unique identifier for this network session, assigned when spawned. |
|__observers__ |The list of client NetworkConnections that are able to see this object. This is read-only. |
|__playerControllerId__ |The identifier of the controller associated with this object. Only valid for player objects. |
|__sceneId__ |A unique identifier for networked objects in a scene. This is only populated in play-mode. |
|__serverOnly__ |A flag to make this object not be spawned on clients. |

Hints
-----
* Put a NetworkIdentity component on prefabs that will be spawned.
* A NetworkIdentity is required for every object that is networked.