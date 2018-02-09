Network Manager
===============

(This class is part of the old networking system and is deprecated. See [NetworkManager](ScriptRef:Networking.NetworkManager.html) for the new networking system).

The __Network Manager__ contains two very important properties for making Networked multiplayer games.


![The Network Manager](../uploads/Main/NetworkSet.png) 

You can access the Network Manager by selecting __Edit &gt; Project Settings &gt; Network__ from the menu bar.


Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Debug Level__ |The level of messages that are printed to the console |
|__Sendrate__ |Number of times per second that data is sent over the network |


Details
-------


Adjusting the Debug Level can be enormously helpful in fine-tuning or debugging your game's networking behaviors. When it is set to **0**, only errors from networking will be printed to the console.

The data that is sent at the __Sendrate__ intervals (1 second / __Sendrate__ = interval) will vary based on the __Network View__ properties of each broadcasting object. If the Network View is using __Unreliable__, its data will be send at each interval. If the Network View is using __Reliable Delta Compressed__, Unity will check to see if the Object being watched has changed since the last interval. If it has changed, the data will be sent.
