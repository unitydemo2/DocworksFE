# Navigation Options

![](../uploads/Main/UI_SelectableNavigation.png)

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Navigation__ | The Navigation options refers to how the navigation of UI elements in play mode will be controlled. |
|__None__ | No keyboard navigation.  Also ensures that it does not receive focus from clicking/tapping on it.  |
|__Horizontal__ | Navigates Horizontally. |
|__Vertical__ | Navigates Vertically. |
|__Automatic__ | Automatic Navigation. |
|__Explicit__ | In this mode you can explicitly specify where the control navigates to for different arrow keys. |
|__Visualize__ | Selecting Visualize gives you a visual representation of the navigation you have set up in the scene window. See below. |

![](../uploads/Main/UI_SelectableNavigationExplicit.png)

![Scene window showing the visualized navigation connections](../uploads/Main/GUIVisualizeNavigation.png)

In the above visualization mode, the arrows indicate how the change of focus is set up for the collection of controls as a group. That means - for each individual UI control - you can see which UI control will get focus next, if the user presses an arrow key when the given control has focus. So in the example shown above, If the "button" has focus and the user presses the right arrow key, the first (left-hand) vertical slider will then become focused. Note that the vertical sliders can't be focused-away-from using up or down keys, because they control the value of the slider. The same is true of the horizontal sliders and the left/right arrow keys.