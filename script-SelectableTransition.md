# Transition Options

Within a selectable component there are several transition options depending on what state the selectable is currently in. The different states are: normal, highlighted, pressed and disabled. 

![](../uploads/Main/UI_SelectableTransition.png)



|**_Transition Options:_** |**_Function:_** |
|:---|:---|
|__None__ | This option is for the button to have no state effects at all.|
|__Color Tint__ | Changes the colour of the button depending on what state it is in. It is possible to select the colour for each individual state. It is also possible to set the Fade Duration between the different states. The higher the number is, the slower the fade between colors will be. |
|__Sprite Swap__ | Allows different sprites to display depending on what state the button is currently in, the sprites can be customised.|
|__Animation__ | Allows animations to occur depending on the state of the button, an animator component must exist in order to use animation transition. It’s important to make sure root motion is disabled. To create an animation controller click on generate animation (or create your own) and make sure that an animation controller has been added to the animator component of the button.|

Each Transition option (except None) provides additional options for controlling the transitions. We'll go into details with those in each of the sections below.


##Color Tint

![](../uploads/Main/UI_SelectableColorTint.png)

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Target Graphic__ | The graphic used for the interaction component.|
|__Normal Color__ |The normal color of the control  |
|__Highlighted Color__ |The color of the control when it is highlighted  |
|__Pressed Color__ |The color of the control when it is pressed  |
|__Disabled Color__ |The color of the control when it is disabled  |
|__Color Multiplier__ | This multiplies the tint color for each transition by its value. With this you can create colors greater than 1 to brighten the colors (or alpha channel) on graphic elements whose base color is less than white (or less then full alpha). |
|__Fade Duration__ |The time taken, in seconds,  to fade from one state to another  |


##Sprite Swap

![](../uploads/Main/UI_SelectableSpriteSwap.png)

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Target Graphic__ | The normal sprite to use |
|__Highlighted Sprite__ | Sprite to use when the control is highlighted |
|__Pressed Sprite__ | Sprite to use when the control is pressed |
|__Disabled Sprite__ | Sprite to use when the control is disabled |


##Animation

![](../uploads/Main/UI_SelectableAnimation.png)

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Normal Trigger__ | The normal animation trigger to use |
|__Highlighted Trigger__ | Trigger to use when the control is highlighted |
|__Pressed Trigger__ | Trigger to use when the control is pressed |
|__Disabled Trigger__ | Trigger to use when the control is disabled |
