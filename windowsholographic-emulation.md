# Holographic Emulation

Holographic Emulation allows you to prototype, debug, and run Microsoft HoloLens projects directly in the Unity Editor rather than building and running the game every time you want to see the effect of a change. This vastly reduces time between iterations when developing holographic applications in Unity.

![Holopgraphic Emulation: The Unity Editor runs as a holographic application ](../uploads/Main/HolographicEmulation-0.gif)

Holographic Emulation has two different modes:

* __Remote to Device:__ Using a connection to a Windows Holographic device, your application behaves as if it were deployed to that device, while really running in the Unity Editor on your host machine.  See [Remote to Device](#RemoteToDevice), below, for more information.

* __Simulate in Editor:__ Your application runs on a simulated Holographic device directly in the Unity Editor, with no connection to a real-world Windows Holographic device. See [Simulate in Editor](#SimulateInEditor), below, for more information.

Holographic Emulation is supported on any machine running Windows 10 (with the Anniversary update) or later versions.

### Getting started

To enable remoting or simulation, open the Unity Editor and go to __Window__ > __Holographic Emulation__:

![](../uploads/Main/HolographicEmulation-Open-1.png)

This opens the Holographic Emulation control window, containing the __Emulation Mode__ drop-down menu. Keep this window visible during development; you need to be able to access its settings when you launch your application.

![Default __Holographic Emulation__ control window
](../uploads/Main/HolographicEmulation-ControlPanel-2.png)

__Emulation Mode__ is set to __None__ by default, which means that your application runs in the Editor without any of the Holographic API functionality. Change the __Emulation Mode__ to __Remote to Device__ or __Simulate in Editor__ to enable that mode and begin Holographic Emulation.

<a name="RemoteToDevice"> </a>
## Remote to Device

To use this, connect your machine running the Unity Editor (the "host machine") to a Windows Holographic device (the “device”) (see [Connecting your device](#ConnectingYourDevice), below). Your application behaves as if it were deployed to that device, while really running in the Unity Editor on the host machine.

The Unity Editor has access to spatial sensor data and head tracking of the connected device.  The Unity Editor Game View allows you to see what is being rendered on the device but not what the wearer of the device sees of the real world. (See an example in the image above titled 'Holopgraphic Emulation: The Unity Editor runs as a hologrpahic application'.)

Note that __Remote to Device__ isn’t useful for validating performance because your application is running on the host machine, rather than the device itself, but it is a quick way to test development.

To enable this mode in the Unity Editor, set the __Emulation Mode__ to __Remote to Device__. The interface changes to reflect the additional options available.

![Holographic Emulation control window with __Remote to Device__ selected](../uploads/Main/HolographicEmulation-RemoteToDevice-3.png)

<a name="ConnectingYourDevice"> </a>
### Connecting your device

![The Holographic Remoting Player screen on your device
](../uploads/Main/HolographicEmulation-RemotingPlayer-4.png)

1. Install and run the Remoting Player, available from the [Windows Store](https://www.microsoft.com/en-us/store/p/holographic-remoting-player/9nblggh4sv40). When launched, the Remoting Player enters a waiting state and displays the IP address of the device on the Holographic Remoting Player screen.  Find additional information about the Remoting Player, including how to enable connection diagnostics on the [Microsoft Windows Dev Center](https://developer.microsoft.com/en-us/windows/holographic/holographic_remoting_player).

2. In the Holographic Emulation control window in the Unity Editor, enter the IP address of your device into the __Remote Machine__ field. The drop-down button to the right of the field allows you to select recently used addresses.

3. Press the __Connect__ button. The connection status changes to a green light with a connected message. 

4. Now click __Play__ in the Unity Editor to run your device remotely. You can pause, inspect GameObjects, and debug in the same way as running an app in the Editor;  but with video, audio, and device input transmitted back and forth across the network between the host machine and the device.

### Known limitations

* Speech ([PhraseRecognizer](https://docs.unity3d.com/ScriptReference/Windows.Speech.PhraseRecognizer.html)) is not supported via __Remote to Device__; instead, it intercepts speech from the host machine running the Unity Editor.

* While __Remote to Device__ is running, all audio on the host machine redirects to the device, including audio from outside your application.

<a name="SimulateInEditor"> </a>
## Simulate in Editor

Using this, your application runs on a simulated Holographic device directly in the Unity Editor with no connection to a real-world Windows Holographic device. This is useful for development for Windows Holographic if you don’t have access to a device. (Note that you do need to test on a device and not rely on the Emulator.)

To enable this mode, set the __Emulation Mode__ to __Simulate in Editor__ and press the __Play__ button:  Your application starts in a emulator built into the Unity Editor. 

In the Holographic control panel, use the __Room__ drop-down menu to choose from one of five virtual rooms (the same as those supplied with the XDE HoloLens Emulator), and use the __Gesture Hand__ drop-down menu to specify which virtual hand (left or right) performs gestures.

![Holographic Emulation control window with __Simulate in Editor__ selected
](../uploads/Main/HolographicEmulation-SimulateInEditor-5.png)

In __Simulate in Editor__ mode, you need to use a game controller (such as an Xbox 360 or Xbox One controller) to control the virtual human player. If you don’t have a controller, the simulation still works, but you cannot move the virtual human player around. 

|**Control:** |**Function:** |
|:---|:---|
|**Left stick**	|Up and down to move virtual human player backward and forward; left and right to move left and right.|
|**Right stick**	|Up and down to pitch virtual human player’s head up and down; left and right to turn virtual human player left and right.|
|**D-pad**	|Move the virtual human player up and down or roll head left and right.|
|**Left and right trigger buttons; A button**	|Perform a tap gesture with a virtual hand.|
|**Y button**	|Reset the pitch and roll of the virtual human player’s head.|

To use the game controller, the Unity Editor’s focus must be on the Game view. Click the Game view window once after doing anything else with the UI to return the focus to it.

### Known limitations

* Most game controllers work with __Simulate in Editor__ mode, as long as they are recognised by Windows and Unity; however, there may be some incompatibility with unsupported controllers.

* You can use [PhotoCapture](https://docs.unity3d.com/550/Documentation/ScriptReference/VR.WSA.WebCam.PhotoCapture.html) in __Simulate in Editor__ mode, but because there is no device present, you need to do this with your own local camera (such as an attached webcam). This means you cannot retrieve a matrix with `TryGetProjectionMatrix` or `TryGetCameraToWorldMatrix`, because a normal local camera cannot compute where it is in relation to the real world.

