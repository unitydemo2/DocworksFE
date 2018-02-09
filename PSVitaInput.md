PS Vita Input
===

Note that an extensive sample project ("Input and Motion") is available for download from within the Unity for PS Vita release notes.

![](../uploads/Main/psvita_device_front.jpg) 

![](../uploads/Main/psvita_device_rear.jpg) 

### To Query Button states:

* Call ``Input.GetKey()`` with a KeyCode. See table below for reference.

    * eg. Use ``Input.GetKey(KeyCode.Joystick1Button0)`` to see if 'Cross' is pressed.

* Call ``Input.GetButton()`` with a name set in the Input Manager. See table below for reference.

    * eg. Use ``Input.GetButton("ButtonName")`` to see if a button is pressed, where ButtonName refers to a name as set up in the Input Manager.

### To query analog axis values:
* Call ``Input.GetAxis()`` with a name set in the Input manager. See table below for reference.

## Input Settings
The following settings can be used to detect stick and button input on the device.


|**_Button Name_** |**_Positive Button_** |**_Type_** |**_Axis_** |**_KeyCode - Used with Input.GetKey()_** |**_Comments_** |
|:---|:---|
|Cross|joystick button 0|Key or Mouse Button|N/A|Joystick1Button0||
|Circle|joystick button 1|Key or Mouse Button|N/A|Joystick1Button1||
|Square|joystick button 2|Key or Mouse Button|N/A|Joystick1Button2||
|Triangle|joystick button 3|Key or Mouse Button|N/A|Joystick1Button3||
|Left Shoulder|joystick button 4|Key or Mouse Button|N/A|Joystick1Button4||
|Right Shoulder|joystick button 5|Key or Mouse Button|N/A|Joystick1Button5||
|Select|joystick button 6|Key or Mouse Button|N/A|Joystick1Button6||
|Start|joystick button 7|Key or Mouse Button|N/A|Joystick1Button7||
|D-Pad Up|joystick button 8|Key or Mouse Button|N/A|Joystick1Button8||
|D-Pad Right|joystick button 9|Key or Mouse Button|N/A|Joystick1Button9||
|D-Pad Down|joystick button 10|Key or Mouse Button|N/A|Joystick1Button10||
|D-Pad Left|joystick button 11|Key or Mouse Button|N/A|Joystick1Button11||
|Left Stick|N/A|Joystick Axis|X Axis (Horizontal) / Y Axis (Vertical)|N/A|Range [-1; 1]|
|Right Stick|N/A|Joystick Axis|4th Axis (Joysticks) - Horizontal / 5th Axis (Joysticks) - Vertical|N/A|Range [-1; 1]|

## Screen (Touch Screen)
The touchscreen is implemented through the standard Input class. As a quick example, to iterate through each current touch you would use the code:

````
foreach (Touch touch in Input.touches)
{
}
````

## Rear Touch Pad
The rear touch pad is implemented through the PSVitaInput class. For example, to iterate through each of current touch you would use the code:

````
foreach (Touch touch in PSVitaInput.touchesSecondary) 
{
}
````

## Gyroscope
The gyroscope is accessible through the standard Input class.

You can also enabled or disable Tilt Correction and Dead Band Filter using ``PSVitaInput.gyroTiltCorrectionEnabled`` and ``PSVitaInput.gyroDeadbandFilterEnabled``.

## Compass
The compass is accessible through the standard Input class.

## Accelerometer
The accelerometer is accessible through the standard Input class.

