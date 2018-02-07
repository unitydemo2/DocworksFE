# Activation Clip properties

Use the Inspector window to change the name of an Activation clip and its **Clip Timing**.  

![Inspector window when selecting an Activation clip in the Timeline Editor window](../uploads/Main/timeline_inspector_activation_clip.png)

## Display Name

The name of the Activation clip shown in the Timeline Editor window. By default, each Activation clip is named "Active". 

## Clip Timing properties

Use the **Clip Timing** properties to trim and change the duration of the Activation clip. Most of the timing properties are expressed in both seconds (s) and frames (f). When specifying seconds to modify a **Clip Timing** property, all decimal values are accepted. When specifying frames, only integer values are accepted. For example, if you attempt to enter 12.5 in a frames (f) field, it is set to 12 frames.

|**Property:** |**Function:** |
|:---|:---|
|__Start__| The frame or time (in seconds) when the clip starts. Changing the Start property changes the position of the clip on its track in the Timeline Asset. Changing the Start may also affect the Duration. All clips use the Start property. |
|__End__ | The frame or time (in seconds) when the clip ends. Changing the End property affects the Duration. All clips use the End property. |
|__Duration__ | The duration of the clip in frames or seconds. Changing the Duration property also affects the End property. All clips use the Duration property. |

---
* <span class="page-edit">2017-12-07  <!-- include IncludeTextNewPageSomeEdit --></span>