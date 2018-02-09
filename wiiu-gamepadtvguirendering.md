Rendering on Multiple Displays
=====

## Camera

*Camera* component has a *Target Display* property that assigns camera to render to either **TV** or **GamePad**.

![](../uploads/Main/RenderingOnGamepadsAndTv_01.png)

This setting maps to `targetDisplay` property in `Camera` class and can be changed from scripts as follows:

````
GetComponent<Camera>().targetDisplay = WiiU.DisplayIndex.TV;
````

In top-left of *GameView* window, you can find a drop down list of displays that the view refers to.

![](../uploads/Main/RenderingOnGamepadsAndTv_02.png)

## Output Mirroring

You can display the same output on both TV and GamePad using output duplicating. Unity exposes this functionality through `UnityEngine.WiiU.Core` class, `tvSource` and `gamePadSource` properties. Each property defines which output, designated for TV or GamePad, to display on TV or GamePad. Default values are `DisplayIndex.TV` for `tvSource` and `DisplayIndex.GamePad` for GamePad.

````
// Display TV output on GamePad
UnityEngine.WiiU.Core.gamePadSource = UnityEngine.WiiU.DisplayIndex.TV;
````

## GUI

By default any Immediate Mode GUI controls will be rendered on `display 0` only (this behaviour has changed compared to 4.3 where GUI would appear on both TV and GamePad by default). You can control the display that GUI will appear on using a GUITarget attribute attached to OnGUI method. Attribute's constructor expects one or more display indices that the UI widgets will appear on. For your convenience `UnityEngine.WiiU.DisplayIndex` class defines `TV` and `GamePad` constants that map to TV and GamePad respectively.

Render on GamePad display only:

````
[GUITarget(UnityEngine.WiiU.DisplayIndex.GamePad)]
void OnGUI() {
	// code will only render to GamePad
}
````

Both displays:

````
[GUITarget(UnityEngine.WiiU.DisplayIndex.GamePad, UnityEngine.WiiU.DisplayIndex.TV)]
void OnGUI() {
	// code will render to both displays
}
````
