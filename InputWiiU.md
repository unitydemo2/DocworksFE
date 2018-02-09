WiiU Joystick Aliases and Axes
====


On WiiU you have one customer defined and several pre-defined joysticks you can attach to axes in the Editor's InputManager.

###Joysticks

These virtual joysticks can be used in the Editor's InputManager by setting 'Type', 'Axis' and 'JoyNum' of one of the axes.

####Joystick 1

This joystick defaults to the controller on channel 1 but can be dynamically set with the script property 'WiiUInput.mouseController' which also acts as a joystick.
The analog stick of a Nunchuk extension controller attached to that controller will be mapped to x- and y-axis of 'Joystick 1'.

####Joystick 2

This joystick is bound to the GamePad controller.
The controller's buttons correspond to the joystick's buttons as follows:

| | |
|:---|:---|
|__1__|'B' Button|
|__2__|'A' Button|
|__3__|'Y' Button|
|__4__|'X' Button|
|__5__|'ZL' Trigger|
|__6__|'ZR' Trigger|
|__7__|'-' Button|
|__8__|'+' Button|
|__9__|'left' on the d-pad|
|__10__|'right' on the d-pad|
|__11__|'down' on the d-pad|
|__12__|'up' on the d-pad|
|__13__|'L' Trigger|
|__14__|'R' Trigger|
|__15__|left stick's Button|
|__16__|right stick's Button|

The controller's left and right analog sticks are mapped to the first four joystick axes:


| | |
|:---|:---|
|__axis 1 aka X__|left stick's horizontal movement.|
|__axis 2 aka Y__|left stick's vertical movement.|
|__axis 3__|right stick's horizontal movement.|
|__axis 4__|right stick's vertical movement.|

####Joystick 3 and subsequent

Every connected ProController is added as a Joystick. First connected ProController corresponds to "Joystick 3".
Joystick's buttons and axes map exactly the same to the device's buttons and sticks as for the GamePad controller.


###Axes

These symbolic names can be used directly in the InputManager's fields 'Negative Button', 'Positive Button', 'Alt Negative Button' or 'Alt Positive Button'.
The Buttons of the RemoteController set via 'WiiUInput.mouseController' is accessible via following symbolic names:


| | |
|:---|:---|
|__SDLK_UP__|'up' Button of the d-pad|
|__SDLK_DOWN__|'down' Button of the d-pad|
|__SDLK_LEFT__|'left' Button of the d-pad|
|__SDLK_RIGHT__|'right' Button of the d-pad|
|__SDLK_LCTRL__|'A' Button|
|__SDLK_SPACE__|'B' Button|
|__SDLK_LALT__|'1' Button|
|__SDLK_LCTRL__|'2' Button|
|__SDLK_LMETA__|'2' Button|
|__SDLK_a__|'A' Button|
|__SDLK_b__|'B' Button|
|__SDLK_PLUS__|'+' Button|
|__SDLK_MINUS__|'-' Button|
|__SDLK_BUTTON_1__|'1' Button|
|__SDLK_BUTTON_2__|'2' Button|

Also buttons on an attached Nunchuk extension controller are assigned to symbolic names:


| | |
|:---|:---|
|__SDLK_z__|'Z' Button|
|__SDLK_c__|'C' Button|
|__SDLK_RSHIFT__|'Z' Button|
|__SDLK_LSHIFT__|'C' Button|
