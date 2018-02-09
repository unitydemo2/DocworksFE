#Toggle

The __Toggle__ control is a checkbox that allows the user to switch an option on or off.

![A Toggle.](../uploads/Main/UI_ToggleExample.png)

![](../uploads/Main/UI_ToggleInspector.png)

##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Interactable__ | Will this component will accept input? See [Interactable](script-Selectable). |
|__Transition__ | Properties that determine the way the control responds visually to user actions. See [Transition Options](script-SelectableTransition). |
|__Navigation__ | Properties that determine the sequence of controls. See [Navigation Options](script-SelectableNavigation).|
|__Is On__ | Is the toggle switched on from the beginning?  |
|__Toggle Transition__ | The way the toggle reacts graphically when its value is changed. The options are _None_ (ie, the checkmark simply appears or disappears) and _Fade_ (ie, the checkmark fades in or out). |
|__Graphic__ |The image used for the checkmark. |
|__Group__ | The [Toggle Group](script-ToggleGroup) (if any) that this Toggle belongs to. |


##Events

|**_Property:_** |**_Function:_** |
|:---|:---|
|__On Value Changed__ | A [UnityEvent](UnityEvents) that is invoked when the Toggle is clicked. The event can send the current state as a `bool` type dynamic argument. |


##Details

The Toggle control allows the user to switch an option on or off. You can also combine several toggles into a [Toggle Group](script-ToggleGroup) in cases where only one of a set of options should be on at once.

The Toggle has a single event called _On Value Changed_ that responds when the user changes the current value. The new value is passed to the event function as a `boolean` parameter. Typical use cases for Toggles include:

* Switching an option on or off (eg, playing music during a game).
* Letting the user confirm they have read a legal disclaimer.
* Choosing one of a set of options (eg, a day of the week) when used in a Toggle Group.

Note that the __Toggle__ is a parent that provides a clickable area to children.  If the __Toggle__ has no children (or they are disabled) then it is not clickable.
