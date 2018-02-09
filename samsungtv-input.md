#Samsung TV Input

The input mechanism is different depending on the model of TV.

![Touch Remote -- Large clickable touchpad is the main input mechanism](../uploads/Main/samsungtv-remote2013.jpg)

![Air Remote -- Small clickable touchpad with gyro and arrow buttons](../uploads/Main/samsungtv-remote2014.jpg)

**-The 2015 Remote has no touchpad. It has airmouse capabilities as well as a d-pad**

**-The 2016 TV has an IR remote and supports gamepads**

## Detecting Remote Type

You can use **SamsungTV.airMouseConnected** to determine if you have an **Air Remote** or **Touch Remote** connected.

If an **Air Remote** is connected, you can use the [Gyroscope](ScriptRef:Gyroscope.html) data.

## Input Modes

You select one of three input modes.  Each input mode maps to the controller type.

### DPAD
> _SamsungTV.touchPadMode = SamsungTV.TouchPadMode.Dpad;_

**Touch Remote:**

 * Swiping sends keyboard arrow key events.

**Air Remote:**

 * Physical up, down, left and right buttons around the touchpad send keyboard arrow key events.

```
if (Input.GetKeyDown (KeyCode.RightArrow))
{
    // Right DPAD event
}

if (Input.GetKeyDown (KeyCode.Return))
{
    // touchpad clicked
}
```

### Joystick
> _SamsungTV.touchPadMode = SamsungTV.TouchPadMode.Joystick;_

**Touch Remote and Air Remote:**

 * Touchpad works like an analog joystick producing values from -1 to 1 on two axes.
   * Note that the touchpad is much smaller on the Air Remote and may make it difficult to get precise control.
   * For air mouse, you can alternatively use gyro data to get more precision.

```
// Set up axis Touchpad x in input manager as joystick 2 x axis.
Input.GetAxis ("Touchpad x");
// joystick 2 y axis
Input.GetAxis ("Touchpad y");

if (Input.GetKeyDown (KeyCode.Return))
{
    // touchpad clicked
}
```

### Mouse
> _SamsungTV.touchPadMode = SamsungTV.TouchPadMode.Mouse;_

**Touch Remote:**

 * Touchpad controls a mouse cursor like a laptop's touchpad.

**Air Remote:**

 * Placing one finger on the touchpad activates _air mouse mode_.  While in _air mouse mode_, the user can move the mouse cursor around the screen by physically pointing the remote.

```
// Sets the cursor image (cursor is a Texture2D)
Cursor.SetCursor (cursor, Vector2.zero, CursorMode.Auto); 

// Position of the mouse pointer
Vector3 pos = Input.mousePosition;

if (Input.GetMouseButtonDown (0))
{
    // touchpad clicked
}
```

## Exiting a Game

If the user presses the **RETURN / EXIT** key, **KeyCode.Escape** button is pressed and can be caught by your game.  If desired, the game can exit by calling **Application.Quit()**.

A user can directly exit a game by long pressing on the **RETURN / EXIT** key of the remote.  If this occurs, the **OnApplicationQuit** message is sent to user scripts.

## Camera Gestures

Certain TV models have a camera which can detect hand positions.  It is recommended to not use this input method since not all TV models support it.

**SamsungTV.gestureMode** can be set to one of the following:

| | |
|:---|:---|
| **SamsungTV.GestureMode.Off** | _Camera data is ignored (default)_ |
| **SamsungTV.GestureMode.Mouse** | _One hand controls a mouse pointer.  Grabbing clicks mouse 0._ |
| **SamsungTV.GestureMode.Joystick** | _Two hands control two joystick axes._ |
| | - _Joystick 2 Axis 2:  hand 1 x axis_ |
| | - _Joystick 2 Axis 3:  hand 1 y axis_ |
| | - _Joystick 2 Axis 4:  hand 2 x axis_ |
| | - _Joystick 2 Axis 5:  hand 2 y axis_ |
| | _Grabbing activates the following joystick buttons:_ |
| | - _Joystick 2 Button 0:  hand 1 grab_ |
| | - _Joystick 2 Button 1:  hand 2 grab_ |
| **SamsungTV.gestureWorking** | _Returns true if the camera currently sees at least 1 hand._ |

## Gamepad Input

You can use gamepad input as you would on [any other platform](ScriptRef:Input.html). Here is the mapping for Samsung TV:

| **Buttons (Key or Mouse Button)**	| **Axis (Joystick Axis)** |
|:---|:---|
| joystick button 0 = A	| X axis = Left analog X |
| joystick button 1 = B	| Y axis = Left analog Y |
| joystick button 2 = X	| 3rd axis = LT (-1 to 1) |
| joystick button 3 = Y	| 4th axis = RT (-1 to 1) |
| joystick button 4 = LB | 5th axis = Right analog X |
| joystick button 5 = RB | 6th axis = Right analog Y |
| joystick button 6 = Back | 7th axis = Dpad X |
| joystick button 7 = Start | 8th axis = Dpad Y |
| joystick button 8 = Left analog press | |
| joystick button 9 = Right analog press | |

### Gamepad Mouse Mode

The gamepad can also be put into mouse pointer mode where the analog stick controls the mouse position and button 0 clicks the mouse 0.

**SamsungTV.gamePadMode** can be one of the following:

| | |
|:---|:---|
| **SamsungTV.GamePadMode.Default** | _Standard joystick input_ |
| **SamsungTV.GamePadMode.Mouse** | _Mouse style input: gamepad analog stick controls a mouse cursor, button 0 clicks mouse 0._ |

