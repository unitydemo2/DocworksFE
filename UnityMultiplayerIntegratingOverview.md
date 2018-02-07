#Integrating the Multiplayer Service

There are three different methods you can use to start working with the Multiplayer Service in your project. These three methods give you a different level of control depending on your needs.

- using NetworkManagerHUD. (simplest, requires no scripting)
- using NetworkServer and NetworkClient. (high-level, simpler scripting)
- using NetworkTransport directly. (low-Level, more complex scripting)

The first method, using __NetworkManagerHUD__ offers the highest level of abstraction, meaning that the Service does most of the work for you. This is therefore the simplest method to use, and most suitable for those new to creating multiplayer games. It provides a simple graphical interface which you can use to perform the basic multiplayer tasks of creating, listing, joining and starting games (referred to as 'matches').

The second method, using __NetworkServer__ and __NetworkClient__, uses our [Networking High-Level API](UNetUsingHLAPI) to do these same tasks. This method is more flexible; you can use the examples provided to integrate the basic multiplayer tasks into your games own UI.

The third method, using _NetworkTransport_ directly, gives you maximum control, but is only usually necessary if you have unusual requirements which are not met by using our [Networking High-Level API](UNetUsingHLAPI).