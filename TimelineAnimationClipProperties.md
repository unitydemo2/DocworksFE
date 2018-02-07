# Animation Clip common properties

Use the Inspector window to change the common properties of an Animation clip. The common properties of an Animation Clip include its name, its timing, play speed, its blend properties, and its extrapolation settings.

![Inspector window when selecting an Animation clip in the Timeline Editor window](../uploads/Main/timeline_inspector_animation_clip_common.png)

## Display Name

The name of the Animation clip shown in the Timeline Editor window. 

## Clip Timing properties

Use the **Clip Timing** properties to trim, change the duration, change the ease-in and ease-out duration or extrapolation, and to adjust the play speed of the Animation clip. 

Most of the following timing properties are expressed in both seconds (s) and frames (f). When specifying seconds to modify a **Clip Timing** property, all decimal values are accepted. When specifying frames, only integer values are accepted. For example, if you attempt to enter 12.5 in a frames (f) field, it is set to 12 frames.

|**Property:** |**Function:** |
|:---|:---|
|__Start__| The frame or time (in seconds) when the clip starts. Changing the Start property changes the position of the clip on its track in the Timeline Asset. Changing the Start may also affect the Duration. |
|__End__ | The frame or time (in seconds) when the clip ends. Changing the End property affects the Duration. All clips use the End property. |
|__Duration__ | The duration of the clip in frames or seconds. Changing the Duration property also affects the End property. |
|__Ease In Duration__ | Sets the number of seconds or frames that it takes for the clip to ease in. If the beginning of the clip overlaps and blends with another clip, the Ease In Duration cannot be edited and instead shows the duration of the blend between clips. See [Blending clips](TimelineBlendingClips). |
|__Ease Out Duration__ | Sets the number of seconds or frames that it takes for the clip to ease out. If the end of the clip overlaps and blends with another clip, the Ease Out Duration cannot be edited and instead shows the duration of the blend between clips. In this case, trim or position the clip to change the duration of the blend between clips. See [Blending clips](TimelineBlendingClips). |
|__Clip In__ | Sets the offset of when the source clip should start playing. For example, to play the last 10 seconds of a 30 second audio clip, set Clip In to 20 seconds. |
|__Speed Multiplier__ | A multiplier on the playback speed of the clip. This value must be greater than 0. Changing this value of the clip will change the duration of the clip to play the same content. |

## Animation Extrapolation

Use the **Animation Extrapolation** properties to set the gap extrapolation before and after an Animation clip. The term **gap extrapolation** refers to how an Animation track approximates or extends animation data in the gaps before, between, and after the Animation clips on a track. 

Only Animation clips use the **Animation Extrapolation** properties. There are two properties for [setting the gap extrapolation](TimelineGapExtrapolation) between Animation clips.

|**Property:** |**Function:** |
|:---|:---|
|__Pre-Extrapolate__| Controls how animation data is approximated in the gap before an Animation clip. The Pre-Extrapolate property affects easing-in an Animation clip. |
|__Post-Extrapolate__ | Controls how animation data extends in the gap after an Animation clip. The Post-Extrapolate property affects easing-out an Animation clip. |

## Blend Curves

Use the **Blend Curves** to customize the transition between the out-going clip and the incoming clip when blending between two Animation clips. See [Blending clips](TimelineBlendingClips) for details on how to blend clips and how to customize blend curves.

When [easing-in or easing-out clips](TimelineEasingClips), the **Blend Curves** allow you to customize the curve that eases-in a clip and the curve that eases-out a clip.

---
* <span class="page-edit">2017-12-07  <!-- include IncludeTextNewPageSomeEdit --></span>


