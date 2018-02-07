# Input for OpenVR controllers

For the Unity Editor to support OpenVR tracked controllers, the Unity VR subsystem presents VR controller inputs as separate joysticks. Use the [UnityEngine.Input](ScriptRef:Input) class to access the axis and button values.

OpenVR’s Unity integration doesn't refer to any specific hardware when presenting axis and button states. This page provides the axis and button mappings for the three types of controllers supported by OpenVR: HTC Vive, Oculus Touch, and Valve Knuckles Controllers.

## Naming convention and detection

When properly configured and connected, any OpenVR-compatible controllers are internally named as either __OpenVR Controller - Left__ or __OpenVR Controller - Right__. Access this name through the list returned by [UnityEngine.Input.GetJoystickNames()](ScriptRef:Input.GetJoystickNames). When available, these controllers appear highlighted in green in the SteamVR status menu when tested with Steam. To access this menu you must have both Steam and SteamVR installed and running on your machine.

![Steam VR status menu](../uploads/Main/steamvr_status_menu.jpg)

You can test the availability of these controllers by periodically checking for their presence in the list of joystick names through script. When the controllers turn off, or when you remove their batteries, an empty string replaces their name in the list returned by [UnityEngine.Input.GetJoystickNames()](ScriptRef:Input.GetJoystickNames). When the controllers turn on again, their name reappears in the list of returned joysticks.

## Unity input system mappings

This section provides diagrams for each type of controller supported by OpenVR devices, along with information on the internal Unity input mapping for each controller button.

### HTC Vive controllers

The diagram below displays the different inputs available on HTC Vive controllers for use in VR applications.

![HTC Vive controller inputs mapping (Image courtesy of developer.viveport.com)](../uploads/Main/vive_controllers.png)


| 1| Menu Button |
|:---|:---| 
| 2| Trackpad |
| 3| System button |
| 4| Status light |
| 5| Micro-USB port |
| 6| Tracking sensor |
| 7| Trigger |
| 8| Grip button |



### Oculus Touch controllers

The diagram below displays the different inputs available on Oculus Touch controllers for use in VR applications.

![Oculus Touch controller input mapping (Image courtesy of developer.oculus.com)](../uploads/Main/oculus_touch.png)


### Knuckles controllers

The diagram below displays the different inputs available when using Knuckles controllers in VR applications.

![Valve Knuckles Controller input mapping (Image courtesy of steamcommunity.com)](../uploads/Main/knuckles_controller.png)

The table below lists controller inputs for each OpenVR-supported controller, their interaction types, Unity axis and button IDs, along with the value range for each axis.

|**HTC Vive Controller**| **Oculus Touch Controller** | **Valve Knuckles Controller** | **Interaction Type** | **Unity Button ID** | **Unity Axis ID** | **Unity Axis Value Range** |
|:---|:---|:---|:---|:---|:---|:---| 
| Left Controller Menu Button (1)| Button.Three | Left Controller Inner Face Button | Press | 2 |  |  |
| Right Controller Menu Button (1)| Button.One | Right Controller Inner Face Button | Press | 0 |  |  |
| |  | Left Controller Outer Face Button | Press | 3 |  |  |
| |  | Right Controller Outer Face Button | Press | 1 |  |  |
| Left Controller Trackpad (2)| Button.PrimaryThumbstick | Left Controller Trackpad | Press | 8 |  |  |
| Right Controller Trackpad (2)| Button.SecondaryThumbstick | Right Controller Trackpad | Press | 9 |  |  |
| Left Controller Trackpad (2)| Button.PrimaryThumbstick | Left Controller Trackpad | Touch | 16 |  |  |
| Right Controller Trackpad (2)| Button.SecondaryThumbstick | Right Controller Trackpad | Touch | 17 |  |  |
| Left Controller Trackpad (2)| Axis2D.PrimaryThumbstick | Left Controller Trackpad | Horizontal Movement |  | 1 | –1.0 to 1.0 |
| Left Controller Trackpad (2)| Axis2D.PrimaryThumbstick | Left Controller Trackpad | Vertical Movement |  | 2 | –1.0 to 1.0 |
| Right Controller Trackpad (2)| Axis2D.SecondaryThumbstick | Right Controller Trackpad | Horizontal Movement |  | 4 | –1.0 to 1.0 |
| Right Controller Trackpad (2)| Axis2D.SecondaryThumbstick | Right Controller Trackpad | Vertical Movement |  | 5 | –1.0 to 1.0 |
| Left Controller Trigger (7)| Axis1D.PrimaryIndexTrigger | Left Controller Trigger | Touch | 14 |  |  |
| Right Controller Trigger (7)| Axis1D.SecondaryIndexTrigger | Right Controller Trigger | Touch | 15 |  |  |
| Left Controller Trigger (7)| Axis1D.PrimaryIndexTrigger | Left Controller Trigger | Squeeze |  | 9 | 0.0 to 1.0 |
| Right Controller Trigger (7)| Axis1D.SecondaryIndexTrigger | Right Controller Trigger | Squeeze |  | 10 | 0.0 to 1.0 |
| Left Controller Grip Button (8)| Axis1D.PrimaryHandTrigger | Left Controller Grip Average | Squeeze |  | 11 | 0.0 to 1.0 |
| Right Controller Grip Button (8)| Axis1D.SecondaryHandTrigger | Right Controller Grip Average | Squeeze |  | 12 | 0.0 to 1.0 |
| |  | Left Controller Index Finger Cap Sensor |  |  | 20 | 0.0 to 1.0 |
| |  | Right Controller Index Finger Cap Sensor |  |  | 21 | 0.0 to 1.0 |
| |  | Left Controller Middle Finger Cap Sensor |  |  | 22 | 0.0 to 1.0 |
| |  | Right Controller Middle Finger Cap Sensor |  |  | 23 | 0.0 to 1.0 |
| |  | Left Controller Ring Finger Cap Sensor |  |  | 24 | 0.0 to 1.0 |
| |  | Right Controller Ring Finger Cap Sensor |  |  | 25 | 0.0 to 1.0 |
| |  | Left Controller Pinky Finger Cap Sensor |  |  | 26 | 0.0 to 1.0 |
| |  | Right Controller Pinky Finger Cap Sensor |  |  | 27 | 0.0 to 1.0 |



Note: Any hardware features not listed in the table above are not exposed through the OpenVR API and are therefore not exposed through Unity’s input system.

## Important controller differences

When developing applications to support OpenVR devices, it is important to note certain differences in input event triggers and response rates for buttons on all three controllers.

Unity Touch Input events differ for each platform controller:

* The [Event System](EventSystem) generates Input Touch events for the triggers on HTC Vive controllers when the user begins squeezing the trigger.
* The [Event System](EventSystem) generates Input Touch events for the triggers on Oculus Touch and Valve Knuckles controllers when [Unity Input](ScriptRef:Input) detects a touch - no trigger squeeze is necessary.


The grip trigger differs between platforms:

* The HTC Vive controllers each have two grip buttons but both map to the same axis. The value for these buttons is 0.0 when not pressed and 1.0 when pressed (intermediate values between 0.0 and 1.0 are not possible).

* The grip on the Oculus Touch Controller is an analog trigger with a range from 0.0 to 1.0 (intermediate values are possible).

* The grip on the Valve Knuckles Controller is a weighted average of the input values for each of the individual finger touch sensors.

