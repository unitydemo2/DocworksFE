#Input Manager

The __Input Manager__ is where you define all the different input axes and game actions for your project.

![The Input Manager](../uploads/Main/InputSetAll.png) 

To see the Input Manager choose: __Edit-&gt;Project Settings-&gt;Input__.


##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Axes__ |Contains all the defined input axes for the current project: __Size__ is the number of different input axes in this project, __Element 0, 1, ...__ are the particular axes to modify. |
|__Name__ |The string that refers to the axis in the game launcher and through scripting. |
|__Descriptive Name__ |A detailed definition of the __Positive Button__ function that is displayed in the game launcher. |
|__Descriptive Negative Name__ |A detailed definition of the __Negative Button__ function that is displayed in the game launcher. |
|__Negative Button__ |The button that will send a negative value to the axis. |
|__Positive Button__ |The button that will send a positive value to the axis. |
|__Alt Negative Button__ |The secondary button that will send a negative value to the axis. |
|__Alt Positive Button__ |The secondary button that will send a positive value to the axis. |
|__Gravity__ |How fast will the input recenter. Only used when the __Type__ is __key / mouse button__. |
|__Dead__ |Any positive or negative values that are less than this number will register as zero. Useful for joysticks. |
|__Sensitivity__ |For keyboard input, a larger value will result in faster response time. A lower value will be more smooth. For Mouse delta the value will scale the actual mouse delta. |
|__Snap__ |If enabled, the axis value will be immediately reset to zero after it receives opposite inputs. Only used when the __Type__ is __key / mouse button__. |
|__Invert__ |If enabled, the positive buttons will send negative values to the axis, and vice versa. |
|__Type__ |Use __Key / Mouse Button__ for any kind of buttons, Mouse Movement for mouse delta and scrollwheels, __Joystick Axis__ for analog joystick axes and __Window Movement__ for when the user shakes the window. |
|__Axis__ |Axis of input from the device (joystick, mouse, gamepad, etc.) |
|__Joy Num__ |Which joystick should be used. By default this is set to retrieve the input from all joysticks. This is only used for input axes and not buttons. |


##Details

All the axes that you set up in the Input Manager serve two purposes:

* They allow you to reference your inputs by axis name in scripting
* They allow the players of your game to customize the controls to their liking

All defined axes will be presented to the player in the game launcher, where they will see its name, detailed description, and default buttons. From here, they will have the option to change any of the buttons defined in the axes. Therefore, it is best to write your scripts making use of axes instead of individual buttons, as the player may want to customize the buttons for your game.


![The game launcher's Input window is displayed when your game is run](../uploads/Main/Input-GameLauncher.png) 

See also: [Input](Input).
