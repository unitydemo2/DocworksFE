#Settings menu

The __Settings__ menu is located in the top left of the Look Dev view. This contains all of the global options for Look Dev.

![](../uploads/Main/LookDevSettings.png)

__Multi-view__

|**Property** |**Function** |
|:---|:---|
| __Single__ |A single-screen view of Look Dev.|
| __Side by side__ |Duplicated view, displayed side by side.|
| __Split-screen__ |Splits the view horizontally in two. An orange/blue manipulation Gizmo represents the separation plane between the two views.|
| __Zone__ |Splits the view in two, with a circular split defined by the positioning of the orange/blue manipulation Gizmo.|

__Camera__

|**Property** |**Function** |
|:---|:---|
| __Fit View__ |Click this to reset the position of the objects to the center of the view (or views, if there are multiple views).|
| __Enable Tone Mapping__ |Click this to toggle the built-in tone mapper. This tone mapper is not an artistic tone mapper but a neutral one which conserves the range but doesn’t include any film effects.|
| __Exposure Range__ |Use this to define the minimum and maximum range of the Exposure Value (EV) slider in the [Control Panel](LookDevControlPanel) and [Views menu](LookDevViewsMenus) (up to a maximum of 32). Useful for testing an extreme light source in the HDRI.|

__Lighting__

|**Property** |**Function** |
|:---|:---|
| __Enable Shadows__ |Click this to toggle Environment Shadow off and on.|
| __Shadow distance__ |Use this to set the maximum shadow distance for the Environment Shadow. If this is set to 0, an automatic number is defined based on Mesh bounds.|

__Animation__

|**Property** |**Function** |
|:---|:---|
| __Rotate Objects__ |Enable this to make an Asset or GameObject continuously rotate in the Look Dev view.|
| __Rotate environment__ |Enable this to make the HDRI environment continuously rotate in the Look Dev view.|
| __Rotate Objects speed__ |Use this to set the speed of the GameObject’s rotation (if __Rotate Objects__ is enabled).|
| __Rotate Env. speed__ |Use this to set the speed of the environment’s rotation (if __Rotate environment__ is enabled).|

__Viewport__

|**Property** |**Function** |
|:---|:---|
| __Reset View__ |Click to reset the __Camera__ settings and __View__ settings.|

__HDRI Library__

|**Property** |**Function** |
|:---|:---|
| __Save Current Library__ |Select this to save the current HDRI Library.|
| __Save As New Library__ |Select this to save the current HDRI Library to a new Asset Library.|
| __Load Library__ |Load a previously saved HDRI Library. The field here displays the name of the current HDRI Library Asset that has been loaded.|

__Misc__

|**Property** |**Function** |
|:---|:---|
| __Show Chrome/grey ball__ | Enable this to display a chrome ball and a grey ball in the bottom left of the screen (see image below). This is useful for debugging reflections and checking the average lighting reference.|
| __Show Controls__ | Enable this to display the [Control Panel](LookDevControlPanel) in the Look Dev view.|
| __Allow Different Objects__ |Enable this to load two different GameObjects when in multi-view mode.|
| __Resynchronise Objects__ |Use this to assign the current GameObject in your selected view to the other view.|

![The user interface with __Show Chrome/grey ball__  enabled](../uploads/Main/LookDev-ChromeGreyBall.png)