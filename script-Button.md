#Button

The __Button__ control responds to a click from the user and is used to initiate or confirm an action. Familiar examples include the _Submit_ and _Cancel_ buttons used on web forms.

![A Button.](../uploads/Main/UI_ButtonExample.png)

![](../uploads/Main/UI_ButtonInspector.png)

##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Interactable__ | Will this component will accept input? See [Interactable](script-Selectable). |
|__Transition__ | Properties that determine the way the control responds visually to user actions. See [Transition Options](script-SelectableTransition). |
|__Navigation__ | Properties that determine the sequence of controls. See [Navigation Options](script-SelectableNavigation).|

##Events

|**_Property:_** |**_Function:_** |
|:---|:---|
|__On Click__ | A [UnityEvent](UnityEvents) that is invoked when when a user clicks the button and releases it. |


##Details

The button is designed to initiate an action when the user clicks and releases it. If the mouse is moved off the button control before the click is released, the action does not take place.

The button has a single event called _On Click_ that responds when the user completes a click. Typical use cases include:

* Confirming a decision (eg, starting gameplay or saving a game)
* Moving to a sub-menu in a GUI
* Cancelling an action in progress (eg, downloading a new scene)

