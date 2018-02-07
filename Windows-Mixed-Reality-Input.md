# Input for Windows Mixed Reality

![](../uploads/Main/Windows_logo.png)![](../uploads/Main/Windows_MR_Controllers_image.png)

Windows Mixed Reality motion controllers allow users to interact in Mixed Reality applications, allowing precise, low latency tracking of movement within the field of view (FOV) of their Windows Mixed Reality headset. This is achieved using the sensors built into the headset.

To allow native Unity Editor support for Windows Mixed Reality input hardware, the Unity VR subsystem presents three inputs as separate joysticks. Use the [UnityEngine.Input](ScriptRef:Input.html) class to read the axis and button values of these inputs.

## __Controller naming conventions and detection__

When properly configured and connected to your computer, the motion controllers appear in the list returned by [UnityEngine.Input.GetJoystickNames()](ScriptRef:Input.GetJoystickNames.html) as __Spatial Controller - Left__ and __Spatial Controller - Right__. For information on correctly configuring and connecting the motion controllers, see the [Windows Developer Center documentation](https://developer.microsoft.com/en-us/windows/mixed-reality/motion_controllers).

In Unity you can check the availability of the controllers through script by periodically checking for their presence in the list of joystick names. When the controllers are turned off, or their batteries are removed, an empty string replaces their name in the list returned by [UnityEngine.Input.GetJoystickNames()](ScriptRef:Input.GetJoystickNames.html). When the controllers are turned back on, their name re-appears in the list.

## __Unity Input system mappings__

The image below shows the buttons available on your Windows Mixed Reality controller.

![Windows Mixed Reality Controller buttons (image courtesy of developer.microsoft.com)](../uploads/Main/Input_mapping.png)

The table below shows the interaction types, button IDs, axis and value ranges for each input provided by the controller in Unity.

| __Hardware Feature__| __Interaction Type__ | __Unity Button ID__ | __Unity Axis ID__ | __Unity Axis Value Range__ |
|:---|:---|:---|:---|:---| 
| Touchpad| Touch | Left: 18<br/>Right: 19 | - | - |
| Touchpad| Press | Left: 16<br/>Right: 17 | - | - |
| Touchpad| Horizontal Movement | - | Left: 17<br/>Right: 19 | -1.0 to 1.0 |
| Touchpad| Vertical Movement | - | Left: 18<br/>Right: 20 | -1.0 to 1.0 |
| Thumbstick| Press | Left: 8<br/>Right: 9 | - | - |
| Thumbstick| Horizontal Movement | - | Left: 1<br/>Right: 4 | -1.0 to 1.0 |
| Thumbstick| Vertical Movement | - | Left: 2<br/>Right: 5 | -1.0 to 1.0 |
| Select Trigger| Press | Left: 14<br/>Right: 15 | - | - |
| Select Trigger| Squeeze | - | Left: 9<br/>Right: 10 | 0.0 to 1.0 |
| Grip button| Press | Left: 4<br/>Right: 5 | - | - |
| Grip button| Squeeze | - | Left: 11<br/>Right: 12 | 0.0 and 1.0* |
| Menu button| Press | Left: 6<br/>Right: 7 | - | - |

Windows Mixed Reality controller input details for Unity

*The Grip squeeze axis is a binary control, so it only reports values of 0 or 1, with no values in between.

The table below lists the different axes available when using Window Mixed Reality controller inputs, along with the positive and negative directions for each axis.

| __Axis__| __Positive Direction__ | __Negative Direction__ |
|:---|:---|:---| 
| Horizontal| To the left. | To the right. |
| Vertical| Up | Down |



Positive and negative directions for Windows Mixed Reality controller input axes in Unity

For further details on using the Windows MR motion controllers with Unity, visit the [Windows developer center section on Motion Controllers in Unity](https://developer.microsoft.com/en-us/windows/mixed-reality/gestures_and_motion_controllers_in_unity).

---
* <span class="page-edit">2017-11-21 <!-- include IncludeTextNewPageYesEdit --></span>

* <span class="page-history">New functionality in 2017.2</span>

