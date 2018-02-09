#Input for OpenVR controllers

To facilitate Unity Editor native support for tracked controllers supported by OpenVR, the Unity VR subsystem presents VR controller inputs as separate joysticks. You can access their axis and button values with the [UnityEngine.Input](ScriptRef:Input.html) class. 

By using OpenVR's controller abstraction, the Unity Editor presents axis and button states in a hardware-agnostic approach (that is, it doesn’t refer to any specific hardware, but uses generic terms). However, for the sake of clarity, the axis and button mappings given below are for the two supported controller types: the HTC Vive controllers, and the Oculus Touch Controllers.

##Naming convention and detection
When properly configured and connected, a pair of Oculus Touch Controllers or a pair of HTC Vive controllers appear in the list returned by [UnityEngine.Input.GetJoystickNames()](ScriptRef:Input.GetJoystickNames.html) as __OpenVR Controller - Left__ and __OpenVR Controller - Right__. When available, these controllers appear highlighted in green in the SteamVR status window.

Unity script code can test for the availability of these controllers by periodically checking for their presence in the list of joystick names. When the controllers are turned off or have their batteries removed, an empty string replaces their name in the list returned by [UnityEngine.Input.GetJoystickNames()](ScriptRef:Input.GetJoystickNames.html). When the controllers are turned on again, their name appears in the list of returned joysticks.

##Unity Input system mappings

###Diagram of Vive controllers

![(Image courtesy of developer.viveport.com)](../uploads/Main/OculusControllersViveControllers.png)

###Diagram of Oculus Touch Controllers

![(Image courtesy of developer.oculus.com)](../uploads/Main/OculusControllersTouchControllers.png)

| __Vive Controller Hardware Feature__| __Touch Controller Hardware Feature__ | __Interaction Type__ | __Unity Button ID__ | __Unity Axis ID__ | __Unity Axis Value Range__ |
|:---|:---|:---|:---|:---|:---| 
| Left Controller Menu Button (1)| Button.Three | Press | 2 |   |   |
| Right Controller Menu Button (1)| Button.One | Press | 0 |   |   |
| Left Controller Trackpad (2)| Button.PrimaryThumbstick | Press | 8 |   |   |
| Right Controller Trackpad (2)| Button.SecondaryThumbstick | Press | 9 |   |   |
| Left Controller Trackpad (2)| Button.PrimaryThumbstick | Touch | 16 |   |   |
| Right Controller Trackpad (2)| Button.SecondaryThumbstick | Touch | 17 |   |   |
| Left Controller Trackpad (2)| Axis2D.PrimaryThumbstick | Horizontal Movement |   | 1 | -1.0 to 1.0 |
| Left Controller Trackpad (2)| Axis2D.PrimaryThumbstick | Vertical Movement |   | 2 | -1.0 to 1.0 |
| Right Controller Trackpad (2)| Axis2D.SecondaryThumbstick | Horizontal Movement |   | 4 | -1.0 to 1.0 |
| Right Controller Trackpad (2)| Axis2D.SecondaryThumbstick | Vertical Movement |   | 5 | -1.0 to 1.0 |
| Left Controller Trigger (7)| Axis1D.PrimaryIndexTrigger | Touch | 14 |   |   |
| Right Controller Trigger (7)| Axis1D.SecondaryIndexTrigger | Touch | 15 |   |   |
| Left Controller Trigger (7)| Axis1D.PrimaryIndexTrigger | Squeeze |   | 9 | 0.0 to 1.0 |
| Right Controller Trigger (7)| Axis1D.SecondaryIndexTrigger | Squeeze |   | 10 | 0.0 to 1.0 |
| Left Controller Grip Button (8)| Axis1D.PrimaryHandTrigger | Squeeze |   | 11 | 0.0 to 1.0 |
| Right Controller Grip Button (8)| Axis1D.SecondaryHandTrigger | Squeeze |   | 12 | 0.0 to 1.0 |


**Notes:**

* Touch events differ between platforms:
    * Touch events related to the HTC Vive controller's trigger are only generated once the user begins squeezing the trigger. 
    * Touch events on the Oculus Touch's trigger occur when a touch is detected - no squeeze is necessary.
* The grip trigger differs between platforms:
    * The HTC Vive controller has grip buttons on either side but both map to the same axis. The value is 0.0 when not pressed and 1.0 when pressed with no intermediate values possible.
    * The grip on the Oculus Touch Controller is an analog trigger with a range from 0.0 to 1.0.
* Any hardware features not listed in the table above are not exposed through the OpenVR API and are therefore not exposed through Unity's input system.

