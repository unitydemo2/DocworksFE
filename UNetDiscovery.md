Local Discovery
=============================

The NetworkDiscovery component allows Unity games to find each other on a local network. It can broadcast presence and listen for broadcasts, and optionally join matching games using the NetworkManager. This does not work over the internet, only on local networks. This component uses the UDP broadcast feature of the network transport layer.

To use local discovery, create an empty game object in the scene and add the NetworkDiscovery component to it.

![NetworkDiscovery Component](../uploads/Main/UNetDiscovery.png)

Like the NetworkManagerHUD, this component has a default GUI for controlling it. When the game starts hit the "Initialize Broadcast" button to begin.

The component can run in server mode or in client mode. 

When in server mode, it sends out broadcast messages over the network on the specified port. These messages contain the Key and Version of the game - these identify this particular type of game. To avoid conflicts such as you game trying to join a game of a different type, you should customize the value of the Key field.  The component should be run in server mode if a game is being hosted on that machine. When not using the default GUI, the StartAsServer() function makes the component run in server mode.

When in client mode, the component listens for broadcast messages on the specified port. When a message is recieved and the Key in the message matches the Key in the NetworkDiscovery component, this means that a game is available to join on the local network. When not using the default GUI, the StartAsClient() function makes the component run in client mode.

When using the default GUI, a button will appear that will make the client join the game (if a NetworkManager is available).

There is a virtual function on the NetworkDiscovery component that can be implemented to be notified when broadcast messages are recieved.

```
virtual void OnReceivedBroadcast(string fromAddress, string data);
```

Note that you cannot have a NetworkDiscovery server and client running in the same process at the same time.