PSM Input
====

Note that an extensive sample project (Input and Motion unitypackage) is included with your installation of Unity for PSM.

![](../uploads/Main/psm_vita_lineart_front.png) 

![](../uploads/Main/psm_vita_lineart_rear.png) 

## Button assignments

The following table (_Table 1_) shows the key assignments for PS Vita.

|**_name_** |**_enum_** |
|:---|:---|
|&#215; button |KeyCode.JoystickButton0 |
|&#9675; button |KeyCode.JoystickButton1 |
|&#9633; button |KeyCode.JoystickButton2 |
|&#9651; button |KeyCode.JoystickButton3  |
|L button |KeyCode.JoystickButton4 |
|R button |KeyCode.JoystickButton5 |
|SELECT button |KeyCode.JoystickButton6 |
|START button |KeyCode.JoystickButton7 |
|up button |KeyCode.JoystickButton8 |
|right button |KeyCode.JoystickButton9 |
|down button |KeyCode.JoystickButton10 |
|left button |KeyCode.JoystickButton11 |

_Table 1. Button Assignment of PS Vita_

## To query button states

* Call ``Input.GetKey()`` with a KeyCode. See _Table 1_ for reference.

````
    if (Input.GetKey(KeyCode.Joystick1Button0)) {
        // 'Cross' is pressed.
    }
````

* Call ``Input.GetButton()`` with a name set in the [Input Manager](class-InputManager). See _Table 3_ below for reference.

````
    if (Input.GetButton("Jump")) {
        // key assigned to 'Jump' action is pressed.
        // 'Jump' is assigned in the Input Manager.
    }
````

## Axis assignments

The following table (_Table 2_) shows the axis assignments for PS Vita.

|**_name_** |**_axis_** |**_value_** |
|:---|:---|:---|
|left stick horizontal axis |X axis |left: negative, right: positive |
|left stick vertical axis |Y axis |up: negative, down: positive |
|R button |3rd axis |pressing: -1, default: 0 |
|right stick horizontal axis |4th axis |left: negative, right: positive |
|right stick vertical axis |5th axis |up: negative, down: positive |
|right/left button |6th axis |left: -1, right: 1, default: 0 |
|up/down button |7th axis |down: -1, up: 1, default: 0 |
|L button |8th axis |pressing: 1, default: 0 |
|L button |9th axis |pressing: 1, default: 0 |
|R button |10th axis |pressing: 1, default: 0 |

_Table 2. Axis Assignment of PS Vita_

## To query analog axis values

* Call ``Input.GetAxis()`` with a name set in the Input manager. See _Table 2_ for reference.

## Input Manager button assignments

The following settings can be used to detect stick and button input on the device.

|**_name_** |**_positive button_** |**_type_** |
|:---|:---|:---|
|&#215; button |joystick button 0 |Key or Mouse Button |
|&#9675; button |joystick button 1 |Key or Mouse Button |
|&#9633; button |joystick button 2 |Key or Mouse Button |
|&#9651; button |joystick button 3  |Key or Mouse Button |
|L button |joystick button 4 |Key or Mouse Button |
|R button |joystick button 5 |Key or Mouse Button |
|SELECT button |joystick button 6 |Key or Mouse Button |
|START button |joystick button 7 |Key or Mouse Button |
|up button |joystick button 8 |Key or Mouse Button |
|right button |joystick button 9 |Key or Mouse Button |
|down button |joystick button 10 |Key or Mouse Button |
|left button |joystick button 11 |Key or Mouse Button |

_Table 3. Input Manager Button Assignment of PS Vita_


