PS4 Input
======

Note that an extensive sample project ("Input and Motion") is available for download in the release notes.

![](../uploads/Main/Dualshock4InputMap.png) 

**To Query Button states:**

* Call ``Input.GetKey()`` with a KeyCode. See table below for reference.

    * eg. Use ``Input.GetKey(KeyCode.Joystick1Button0)`` to see if 'Cross' is pressed.

* Call``Input.GetButton()`` with a name set in the Input Manager. See table below for reference.

    * eg. Use ``Input.GetButton("ButtonName")`` to see if a button is pressed, where ButtonName refers to a name as set up in the Input Manager.

**To query analog axis valeus:**

* Call ``Input.GetAxis()`` with a name set in the Input manager. See table below for reference.

## Input Settings
The following settings can be used to detect stick and button input on the device:

|**_Button Name_** |**_Positive Button_** |**_Type_** |**_Axis_** |**_KeyCode - Used with Input.GetKey()_** |**_Comments_** |
|:---|:---|
|Cross|joystick button 0|Key or Mouse Button|N/A|Joystick1Button0||
|Circle|joystick button 1|Key or Mouse Button|N/A|Joystick1Button1||
|Square|joystick button 2|Key or Mouse Button|N/A|Joystick1Button2||
|Triangle|joystick button 3|Key or Mouse Button|N/A|Joystick1Button3||
|Left Shoulder|joystick button 4|Key or Mouse Button|N/A|Joystick1Button4||
|Right Shoulder|joystick button 5|Key or Mouse Button|N/A|Joystick1Button5||
|Touch Pad Button|joystick button 6|Key or Mouse Button|N/A|Joystick1Button6||
|Options|joystick button 7|Key or Mouse Button|N/A|Joystick1Button7||
|L3|joystick button 8|Key or Mouse Button|N/A|Joystick1Button8||
|R3|joystick button 9|Key or Mouse Button|N/A|Joystick1Button9||
|D-Pad|N/A|Joystick Axis|6th Axis (Joysticks) - Horizontal / 7th Axis  (Joysticks) - Vertical|N/A|Range [-1; 1]|
|Left Stick|N/A|Joystick Axis|X Axis - Horizontal / Y Axis - Vertical|N/A|Range [-1; 1]|
|Right Stick|N/A|Joystick Axis|4th Axis  (Joysticks) - Horizontal / 5th Axis  (Joysticks) - Vertical|N/A|Range [-1; 1]|

## Touch Pad
The touch pad is implemented through the PS4Input class with ``PS4Input.GetLastTouchData()``. Two simultaneous touches are supported.

## Pad User Details
Information about the user/pad is available via the ``PS4Input.PadGetUsersDetails(padIndex)``.

## Last Gyro
Use ``PS4Input.GetLastGyro(padIndex)`` to get Gyro information about a given controller.

## Last Orientation
Use ``PS4Input.GetLastOrientation(padIndex)`` to get the controller orientation. To reset the currently read orientation use ``PS4Input.PadResetOrientation(padIndex)``.

## Accelerometer
Use ``PS4Input.GetLastAcceleration(padIndex)`` to get the controller accelerometer information.

## Lightbar
The lightbar can be changed through the PS4Input class with ``PS4Input.PadSetLightBar(padIndex)``. Pass in the ID of the controller to change along with Red, Green and Blue values ranging from 0-255. Note that the lights cannot be turned off and have a 5% lower limit of illumination (13/255).

Camera tracking of the controllers is also not guaranteed if you vary from the default colours assigned to each controller, to reset the lightbar to its default color use ``PS4Input.PadResetLightBar(padIndex)``.

## Controller Speaker
To play an [AudioSource](ScriptRef:AudioSource.html) through the speaker on a user's controller, use either of the following functions:

* ``AudioSource.PlayOnDualShock4PadIndex(padIndex)`` to play audio on a specific controller
* ``AudioSource.PlayOnDualShock4(userId)`` to play audio for a specific logged-in user

To find the userId of the player currently using a controller, use ``PS4Input.PadGetUsersDetails(padIndex)`` to return a ``PS4Input.LoggedInUser`` and retrieve the userId from within that.

The audio output will be adjusted by the setting on the audio source including filters and effects, but the audio source cannot play through both the world and the controller simultaneously.

## Pad Vibration
You can set pad vibration using ``UnityEngine.PS4.PS4Input.PadSetVibration(int padIndex, int largeMotor, int smallMotor)``. The maximum value for the ``largeMotor`` and ``smallMotor`` values is 255.