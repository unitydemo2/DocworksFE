#Deploying a Unity Cluster

##Building the Player
There are no special techniques involved in the build process. As long as you build the player with a Cluster-enabled Editor (it requires a special license), the player will have the Cluster-enabled features.

##Launching the Cluster
Distribute a copy of the player to the Master Node machine, and each of the Client Node machines. It is highly recommended to use the same player files all the time to ensure the simulation will not vary. Prepare a batch file for each node to launch the application with the following command line arguments.

These arguments trigger the player to run in Unity Cluster mode:

###Master node
`-server <number of clients> *:<pubport> *:* <timeout>`

- Run this application as the master of the cluster network.
- Specify the number of clients that connect to the master. This does not include the master. The master does not proceed until the number of clients connected has reached the indicated amount.
- `timeout` is optional. You can use it to tell the server how long to wait for signals from the clients before assuming the network is disconnected.

###Client node
`-client <index> <masterip>:<pubport> <clientip>:<clientport> <timeout>`

This run this application as one of the client nodes in the cluster network.

- `index` is the node index for this client in the network. Each Client Node should be assigned a unique index. The index normally relates to the node's position in the display grid.
- `masterip` is the IP address of the Master Node machine. Do not use `localhost`, it does not resolve correctly.
- `clientip` and `clientport` is the IP address and port of the client machine. Use * for both for auto assignment, which is usually the case.
- `pubport` has to be identical to Master Node's setup.
- `timeout` is optional. It can be used to tell the clients how long to wait for server's signal before it assumes it has been disconnected from the network.

###Additional Arguments

-|-
__-force-opengl__ (windows only)|Make the editor use OpenGL for rendering, even if Direct3D is available. Normally Direct3D is used but OpenGL is used if Direct3D 9.0c is not available.
__-logFile &lt;pathname&gt;__|Specify where the Editor or Windows/Linux standalone log file will be written. Handy when user test the cluster rendering locally.

##Testing locally

You can test cluster rendering by running multiple instances of your project on a single machine, launching each with the appropriate command line arguments as shown above.
