#Slider

The __Slider__ control allows the user to select a numeric value from a predetermined range by dragging the mouse. Note that the similar [ScrollBar](script-Scrollbar) control is used for scrolling rather than selecting numeric values. Familiar examples include difficulty settings in games and brightness settings in image editors.

![A Slider.](../uploads/Main/UI_SliderExample.png)

![](../uploads/Main/UI_SliderInspector.png)

##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Interactable__ | Will this component accept input? See [Interactable](script-Selectable). |
|__Transition__ | Properties that determine the way the control responds visually to user actions. See [Transition Options](script-SelectableTransition). |
|__Navigation__ | Properties that determine the sequence of controls. See [Navigation Options](script-SelectableNavigation).|
|__Fill Rect__ | The graphic used for the fill area of the control. |
|__Handle Rect__ | The graphic used for the sliding "handle" part of the control |
|__Direction__ | The direction in which the slider's value will increase when the handle is dragged. The options are _Left To Right_, _Right To Left_, _Bottom To Top_ and _Top To Bottom_. |
|__Min Value__ | The value of the slider when the handle is at its extreme lower end (determined by the _Direction_ property). |
|__Max Value__ | The value of the slider when the handle is at its extreme upper end (determined by the _Direction_ property). |
|__Whole Numbers__ | Should the slider be constrained to integer values? |
|__Value__ | Current numeric value of the slider.  If the value is set in the inspector it will be used as the initial value, but this will change at runtime when the value changes. |

##Events

|**_Property:_** |**_Function:_** |
|:---|:---|
|__On Value Changed__ | A [UnityEvent](UnityEvents) that is invoked when the current value of the Slider has changed. The event can send the current value as a `float` type dynamic argument. The value is passed as a float type regardless of whether the _Whole Numbers_ property is enabled. |


##Details

The value of a Slider is determined by the position of the handle along its length. The value increases from the _Min Value_ up to the _Max Value_ in proportion to the distance the handle is dragged. The default behaviour is for the slider to increase from left to right but it is also possible to reverse this behavior using the _Direction_ property. You can also set the slider to increase vertically by selecting _Bottom To Top_ or _Top To Bottom_ for the _Direction_ property. 

The slider has a single event called _On Value Changed_ that responds as the user drags the handle. The current numeric value of the slider is passed to the function as a `float` parameter. Typical use cases include:

* Choosing a level of difficulty in a game, brightness of a light, etc.
* Setting a distance, size, time or angle.
