#Advanced operations: Using the LLAPI

While the HLAPI is designed to minimize boilerplate code, the Low-Level API (LLAPI) is designed to permit maximum flexibility. In general, using the LLAPI involves creating UnityWebRequests then creating appropriate `DownloadHandlers` or `UploadHandlers`and attaching them to your `UnityWebRequests`.

This section details the options available in the Low-Level API and the scenarios they are intended to address:

* [Creating UnityWebRequests](UnityWebRequest-CreatingUnityWebRequests)
* [Creating UploadHandlers](UnityWebRequest-CreatingUploadHandlers)
* [Creating DownloadHandlers](UnityWebRequest-CreatingDownloadHandlers)

Note that the HLAPI and LLAPI are not mutually exclusive. You can always customize UnityWebRequest objects created via the HLAPI if you need to tweak a common scenario.

For full details on each of the objects described in this section, please refer to the Unity Scripting API.
