# Audio Clip properties

Use the Inspector window to change the properties of an Audio clip. These properties include the name of the clip, its timing, play speed, its blend properties, the audio file used by the Audio clip, and whether Audio clip loops or plays once.

![Inspector window when selecting an Audio clip in the Timeline Editor window](../uploads/Main/timeline_inspector_audio_clip.png)

## Display Name

The name of the Audio clip shown in the Timeline Editor window. This is not the name of the audio file that is used for the waveform. The name of the audio file is part of the **Audio Playable Asset** properties.

## Clip Timing properties

Use the **Clip Timing** properties to trim and change the duration of the Audio clip. Most of the timing properties are expressed in both seconds (s) and frames (f). When specifying seconds to modify a **Clip Timing** property, all decimal values are accepted. When specifying frames, only integer values are accepted. For example, if you attempt to enter 12.5 in a frames (f) field, it is set to 12 frames.

|**Property:** |**Function:** |
|:---|:---|
|__Start__| The frame or time (in seconds) when the clip starts. Changing the Start property changes the position of the clip on its track in the Timeline Asset. Changing the Start may also affect the Duration. All clips use the Start property. |
|__End__ | The frame or time (in seconds) when the clip ends. Changing the End property affects the Duration. All clips use the End property. |
|__Duration__ | The duration of the clip in frames or seconds. Changing the Duration property also affects the End property. All clips use the Duration property. |

## Blend Curves

Use the **Blend Curves** to customize the transition between the out-going clip and the incoming clip when blending between two Audio clips. See [Blending clips](TimelineBlendingClips) for details on how to blend clips and how to customize blend curves.

When easing-in or easing-out clips, the **Blend Curves** allow you to customize the curve that eases-in an Audio clip and the curve that eases-out an Audio clip. See [Easing-in and Easing-out clips](TimelineEasingClips) for details.

## Audio Playable Asset properties

Use the **Audio Playable Asset** properties to select the Audio file used by the Audio clip and to set whether the selected Audio clip loops (**Loop** enabled) or plays once (**Loop** disabled).

---
* <span class="page-edit">2017-12-07  <!-- include IncludeTextNewPageSomeEdit --></span>

