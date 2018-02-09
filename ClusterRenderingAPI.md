
#API

`Camera.SetStereoViewMatrices`
Define the view matrices for both stereo eye. If you use this function, the default transformation applied according to stereoSeparation will stop until you call ResetStereoViewMatrices().

`Camera.SetStereoProjectionMatrices`
Define the projection matrix for both stereo eye. If you use this function, the default "Asymmetric frustum parallel axis projection" will not be apply until you call ResetStereoProjectionMatrices().

`Camera.ResetStereoViewMatrices`
Use the default view matrices on the camera for both stereo eye. Reset the effect of using SetStereoViewMatrices. 

`Camera.ResetStereoProjectionMatrices`
Use the default projection matrix for both stereo eye. Reset the effect of using SetStereoProjectionMatrices .

`ClusterNetwork.isMasterOfCluster`
Check whether the current instance is a master node in the cluster network.

`ClusterNetwork.isDisconnected`
Check whether the current instance is disconnected from the cluster network. What it does is checking for a flag internally, so, this call is inexpensive to call every frame.

- Client node is consider disconnected when it fail to receive any signal within a timeout period.
- Master node is consider disconnected when it fail to recerve any signal from any single client within a timeout period. Master node will consider itself disconnect even only one client node is lost but others still alive.

Disconnected instance will not terminate itself but instead it will continue running detached from the network.

`ClusterInput.AddInput`
Add a new VRPN input entry. The parameters are identical to how you add a input via “Project Setting > Cluster Input”. Input entry added via this method is just valid for the lifetime of the application session. The added entry will not persist like those you added via the “Project Setting > Cluster Input”.

`ClusterInput.EditInput`
Edit an input entry which added via “AddInput”. This function is not able to edit persistent input entry defined at “Project Setting > Cluster Input”.

`ClusterInput.CheckConnectionToServer`
Check the connection status of the device to the VRPN server it connected to.

