#Input for Cluster Rendering

You must set up your Cluster Rendering network so that input to the Master Node is passed on to all Client nodes. To do this, you need to set up the Cluster Input Settings, and use a VRPN server to send that input to all Client nodes.

##The Cluster Input Manager
For all normal input, you must define input mapping in the Cluster Input Manager settings. This can be found in the `Project setting > Cluster Input` menu.

Property:|Function:
-|-
__Size__|Number of cluster input entries
__Name__|Unique name for this entry. Used in script to identify each entry.
__Device Name__|The name of the device which registered to VRPN server.
__Server URL__|The URL to connect to VRPN. Usually “localhost” if server started locally.
__Index__|The index/channel of the device this input entry suppose to connect to.
__Type__|The type of input.
 - __Button__|Device that return a binary result of pressed or not pressed.
 - __Axis__|Device is an analog axis that provides continuous value represented by a float.
 - __Tracker__|Device that provide position and orientation values.
 - __CustomProvidedInput__|A user customized input.

All the entries entered into the Cluster Input Manager settings can be accessed from script via the [ClusterInput class](ScriptRef:ClusterInput). The usage is much alike to Unity's regular Input class; you can read the state of the input every frame with the API and act on it. For examples, see the [ClusterInput Script Reference](ScriptRef:ClusterInput).


##The VRPN server

Whenever you have a project which reads input from the ClusterInput class, a VRPN server has to be present and running with the correct device connected. A VRPN device is identified by it's name and url. Typically, the fully formed URL is something like TrackerA@localhost. TrackerA being the Device Name, localhost being the Server URL defined in the VRPN settting.

For more information about VRPN, visit this website: [http://www.cs.unc.edu/Research/vrpn/](http://www.cs.unc.edu/Research/vrpn/)

If your project does not use the ClusterInput class, and uses *only* **Custom Input** (see below), then you do not need a VRPN server.

##Custom Input
You may want to integrate your input devices directly using the device manufacturer's SDK, by writing a Unity C++ plugin. This plugin will then pass the values to the C# side of your project using interop services. In such a scenario, the inputs will not be syncrhonized to the rest of the cluster. To bridge this, ClusterInput provides a set of commands that can capture these custom input values and replicate them across the entire cluster.

To do this, you must create and configure an Input in the Cluster Input inspector and set the Type to `"User Provided Input"`. On the master node of the cluster, poll for input values from the integrated device as usual and send them into these inputs using one of these APIs: 

 - [ClusterInput.SetAxis](ScriptRef:ClusterInput.SetAxis)
 - [ClusterInput.SetTrackerPosition](ScriptRef:ClusterInput.SetTrackerPosition)
 - [ClusterInput.SetTrackerRotation](ScriptRef:ClusterInput.SetTrackerRotation)
 
These values will then be available to rest of the cluster and also the master node.

