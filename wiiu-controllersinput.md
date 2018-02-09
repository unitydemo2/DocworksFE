Controllers Input
====

Unity Wii U provides a direct access to Wii U specific input devices.

## GamePad
GamePad input buttons and joysticks are mapped to Unity's InputManager class. In addition to that, all functionality related to the GamePad, including behaviour how the OS pre-processes the input data can be accessed through `UnityEngine.WiiU.GamePad` class and its state structure.

`GamePad` is a proxy structure that is used to query and set GamePad settings. It also provides access to `GamePadState` object through `GamePad.state` property. The state object captures the actual state of buttons pressed, joysticks positions, accelerometer, etc.

```
using WiiU = UnityEngine.WiiU;
// Create a proxy object
WiiU.GamePad gp = WiiU.GamePad.access;
gp.StopMotor();

// Get the input state
WiiU.GamePadState state = gp.state;
if (state.gamePadErr == WiiU.GamePadError.None) {
    if (state.IsTriggered(WiiU.GamePadButton.A)) { 
        Debug.Log("Pressed Button A with GamePad");
    }
}
```

## Classic, Pro, MotionPlus, Nunchuk and other controllers
All other controllers are accessed through `UnityEngine.WiiU.Remote` class and its state property. Similarly to `GamePad` type, first you need to create a `Remote` proxy object to access any settings that influence how Wii Remote or extension controller input are processed.

Starting with Unity 5.0, Remote API closely resembles Cafe SDK API. Note that `classic`, `balanceBoard`, `pro` and `nunchuk` properties in `RemoteState` overlap the same memory area. The data validity of those properties depends on the value of `devType` and `dataFormat` properties.

MotionPlus settings are grouped into `UnityEngine.WiiU.MotionPlus` proxy.

```
using WiiU = UnityEngine.WiiU;

void Start()
{
    WiiU.Remote rem = WiiU.Remote.Access(0);
    // Get a proxy object for MotionPlus access
    MotionPlus mp = rem.motionPlus;
    mp.Enable(WiiU.MotionPlusMode.Standard);
    if (mp.mode == WiiU.MotionPlusMode.Off) {
        // failed to enable
    }
}

// Using Wii Remote on channel 1
WiiU.Remote rem = WiiU.Remote.Access(1);

// Read input state
WiiU.RemoteState state = rem.state;

if (state.IsTriggered(WiiU.RemoteButton.A)) // check Wii Remote state
{
	// A button triggered, do something
}

// check for extension controller state
switch (state.devType)
{
	case WiiU.RemoteDevType.MotionPlusClassic:
		// do something with the state.motionPlus part
	case WiiU.RemoteDevType.Classic:
		if (state.classic.IsTriggered(WiiU.ClassicButton.A)) {
			Debug.Log("Pressed Button A with Classic controller");
		}
		break;
		
	case WiiU.RemoteDevType.MotionPlusNunchuk:
		// do something with the state.motionPlus part
	case WiiU.RemoteDevType.Nunchuk:
		bool shouldRumble = (state.nunchuk.accSpeed > m_threshold);
		if (rem.motorRumble != shouldRumble)
			rem.motorRumble = shouldRumble;
		break;
		
	default:
		break;
}
```

## Memory Allocation

Both proxy and state types for GamePad and Remote are structures. This means they will be placed on stack and creating them does not involve managed-heap allocations.


## Migration Guide (4.3 to 5.x)

Several ideas drove the changes for input API. One was to group functions that relate to specific controller's configuration into individual classes (`WiiU.GamePad`, `WiiU.Remote` and `WiiU.MotionPlus`). This mostly affected Wii Remote API, as GamePad access was implemented that way already. Another goal was to make Input API heap allocation-free. To achieve this, both proxy and input-state types are `struct` and will be placed on stack when created. Because of that, there is no need to preallocate proxy object or keep it around.

In the following text `UnityEngine` namespace is omitted what means that `using UnityEngine` is implied. For the 5.x API, because in C# `using _namespace_` doesn't introduce _namespace_ sub-namespaces into the current scope, `using WiiU = UnityEngine.WiiU` is needed. We recommend adding that to using declarations, though `using UnityEngine.WiiU` is also an option. In this case `WiiU.` disappears.

|5.x API 				| 4.x API |  |
|---- 					|-----					|------|
|WiiU.GamePadState 	|WiiUGamePadData and WiiUGamePad | `WiiU.GamePadState` maps directly to VPAD structure from Cafe SDK. Device state accessors, except to test button states have been removed. Use public structure members for that.	|
|WiiU.GamePad			|WiiUGamePadState		| Proxy structure to ask for the actual button state, access rumble motor and to query/configure GamePad input processing settings. Interface itself is mostly unchanged. |
|WiiU.GamePadError |WiiUGamePadError | |
|n/a |WiiUInput				| Functions have been moved to `WiiU.Remote`, `WiiU.GamePad` and `WiiU.MotionPlus`. |
|WiiU.RemoteState |WiiURemote | `WiiU.RemoteState` maps directly to KPAD structore from Cafe SDK. Use this to get Wii Remote acceleration, button states and readings of Nunchuk, Classic Constroller, Balance Board, MotionPlus accessories. |
|WiiU.Remote |WiiURemoteData	and WiiURemote | Proxy structure to query `Wii.RemoteState` and configure Wii Remote input processing. |
|WiiU.NunchukState |WiiUNunchuk | Accessed through `WiiU.RemoteState.nunchunk`, valid only for specific values of `RemoteDevType`. Nunchuk buttons are part of `WiiU.RemoteState`. |
|WiiU.ProControllerState |WiiUProControllerData | Access this structure through `WiiU.RemoteState.pro`. |
|WiiU.ClassicState |WiiUClassicData and WiiUClassic | Access this structure through `WiiU.RemoteState.classic`. |
|WiiU.MotionPlusState |WiiUMotionPlusData and WiiUMotionPlus | MotionPlus readings, accessed through `WiiU.RemoteState.motionPlus`. |
|WiiU.MotionPlus |WiiUInput | Interface to enable/disable and configure MotionPlus accessory. |
|WiiU.RemoteButton |WiiUButton | For enum names `Button` prefix was dropped. |
|WiiU.SensorBarPosition |WiiUSensorBarPosition | |
|WiiU.GamePadButton |WiiUGamePadButton | For enum names `Button` prefix was dropped. |
|WiiU.ProControllerButton |WiiUProControllerButton | For enum names `Button` prefix was dropped. |
|WiiU.ClassicButton |WiiUClassicButton | For enum names `Button` prefix was dropped. |
|WiiU.RemoteDevType |WiiUDevType | `Freestyle` is renamed to `Nunchuk`. |
|WiiU.RemoteError |WiiUErrorStatus | |
|WiiU.RemoteDataFormat |WiiUDataFormat | |
|WiiU.RemotePlayMode |WiiUPlayMode | |
|WiiU.BalanceBoardCommand |WiiUBalanceCommand | | 
|WiiU.BalanceError |WiiUBalanceError | |
|WiiU.BalanceTGCError |WiiUBalanceTGCError | |
|WiiU.BalanceBoardError |n/a | |
|WiiU.MotionPlusMode |WiiUMotionPlusStatus | |
|WiiU.MotionPlusZeroDriftMode |WiiUMotionPlusZeroDriftMode | |
|WiiU.BatteryLevel |WiiUBatteryLevel | |
|WiiU.BalanceBoardState, WiiU.WPADBLStatus, WiiU.BalanceBoardInfo |WiiUBalanceBoardData | `WiiU.BalanceBoardState` is accessed through `WiiU.RemoteState.balanceBoard`. |
|RemoteInfo |WiiUPadInfo | |

WiiU.RemoteState and WiiU.GamePadState has a few helper functions (which are implemented directly in C#) that simplify button state checks. They directly access `hold/trig/release` values. For example this is the implementation of IsTriggered, others act similarly:

```
public bool IsTriggered(RemoteButton buttonId)
{
	return (trig & (int)buttonId) != 0;
}
```

The following table shows how they map to the new names (they follow Cafe SDK naming).

|5.x API | 4.3 API | |
|---- |---- |---- |
|.IsTriggered	|.GetButtonDown	|Tests a bit of `trig` member |
|.IsReleased	|.GetButtonUp		|Tests a bit of `release` member |
|.IsPressed	|.GetButton		|Tests a bit of `hold` member |


## Examples

### 1. Touch position

```
// 4.3

WiiUGamePad gamePad = WiiUInput.GetGamePad();
Vector2 touchPos = new Vector2(gamePad.touch.x, gamePad.touch.y);
```

```
// 5.x
using WiiU = UnityEngine.WiiU;

// ...

WiiU.GamePad gpA = WiiU.GamePad.access; // accessor
WiiU.GamePadState gamePad = gpA.state; // current button and joystick state
Vector2 touchPos = new Vector2(gamePad.touch.x, gamePad.touch.y);
```

### 2. Button states
```
// 4.3

WiiUGamePad gamePad = WiiUInput.GetGamePad ();
bool downButtonA = gamePad.GetButtonDown (WiiUGamePadButton.ButtonA);
bool downButtonZR = gamePad.GetButtonDown (WiiUGamePadButton.ButtonZR);
```

```
// 5.x

using WiiU = UnityEngine.WiiU;

// ...

WiiU.GamePad gpA = WiiU.GamePad.access; // accessor
WiiU.GamePadState gamePad = gpA.state; // current button and joystick state

bool downButtonA = gamePad.IsTriggered (WiiU.GamePadButton.A);
bool downButtonZR = gamePad.IsTriggered (WiiU.GamePadButton.ZR);
```

