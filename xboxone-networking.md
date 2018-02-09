Networking
==========


The Xbox One does not allow unencrypted communications in production. They use an API called **Secure Sockets** to encrypt secure communication between the Xbox One console and other devices (including other Xbox One consoles). The engine wraps the IPsec implementation for you, and once connections have been made, you can use all your standard Unity NetworkView and RPC's as normal. Currently only peer-to-peer is supported.

  However there are additional steps required to make those connections, and they are described below.

Manifest Socket Descriptions
----------------------------


All socket usage must be described in your game's _appmanifest.xml_ file. This lets the Xbox One know ahead of time which ports needs to be opened for communication while your game is running. You can add these descriptions into your Xbox One Player settings by using the <span class="component">Configured Sockets</span> property. The description can be configured by using <span class="inspector">Secure Device Socket Description</span> window. The [Player Settings](xboxone-playersettings) page explains how this property and window work, but you should consult the XDK documentation for more information on what the different description settings do.

* If your project has any socket descriptions bound to port 0 (or not bound to any port) we advise you to delete them.  They are deprecated and will conflict with Multiplayer.
* Mono broadcasts for Script Debugging are on port 58997 UDP - an entry will be added automatically if this is missing and Script Debugging is turned.  The socket description will be set to Initiate/SendDebug, with no template.
* Raknet outgoing connections use Ephemeral ports by default.  If you include the Multiplayer API DLL in your project, we will automatically add the port range "57344-65535" ("57344-58996" if Script Debugging is turned on).  The Socket description will be set to Initiate/SendGameData, and the template name will be "Raknet" and set to InitiateFromMicrosoftConsole/AcceptOnMicrosoftConsole.

Secure Device Address
-------------------------


Every Xbox console has a **Secure Device Address** (SDA).  You cannot connect to another console without their SDA.  You can obtain this SDA using Microsoft's Matchmaking services.  See our Multiplayer Rendezvous API sample or our Multiplayer Plugin documentation for further details.

Secure Tunnel
-------------------------


Once you have obtained the SDA of the remote device, you can use the **Secure Tunnel** API to initiate a connection to it.  Once the tunnel has opened, you can connect to it using UnityEngine.XboxOne.Network.Connect (similar to the existing UnityEngine.Network.Connect function).

For incoming connections you call UnityEngine.XboxOne.Network.InitializeServer("MyConnectionTemplate", maxConnections, myPort); and specify the "Manifest Socket Description" template name and port you'd like to listen on.
You can also register a callback on the SecureTunnelListener to be informed of incoming SecureTunnel connections.

Please see the Multiplayer/Networking sample for a example of both initiating and hosting connections.  Please also see the Matchmaking plugins API documentation for more details.

No Support for IPv6 exclusive Networks
--------------------------------------


Please note many Unity components do not support IPv6 communication (such as Mono Develop, and the Unity profiler).  Therefore we recommend developing on a network that has at least local IPv4 addresses.
This does not affect peer-to-peer Multiplayer since you connect using SDA's (not directly by specifying IP's).

<span class="component">UnityEngine.Network</span> Port Usage
-----------------------------------------------------------


Since you cannot communicate directly with servers over unencrypted connections, functionality like connecting to the facilitator, proxy servers, or even UnityEngine.Network.TestConnection are not available in production.
Xbox One has it's own built-in support for NAT punch-through.
