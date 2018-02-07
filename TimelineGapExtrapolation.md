### Setting gap extrapolation

Gap extrapolation refers to how an Animation track approximates animation data in the gaps before and after an Animation clip.

The main purpose for extrapolating animation data in the gaps between Animation clips is to avoid animation anomalies. Depending on the GameObject bound to the Animation track, these anomalies could be a GameObject jumping between two transformations, or a humanoid character jumping between different poses.

Each Animation clip has two gap extrapolation settings: __pre-extrapolate__, which controls how animation data is approximated in the gap before an Animation clip, and __post-extrapolate__, which controls how animation data extends in the gap after an Animation clip.

By default, both the pre-extrapolate and post-extrapolate settings are set to Hold. This sets the gap before the Animation clip to hold at the animation on the first frame, and the gap after the Animation clip to hold on the animation on the last frame. Icons before and after an Animation clip indicate the selected extrapolation modes.

![Icons indicate the pre-extrapolate and post-extrapolate modes](../uploads/Main/timeline_gap_extrap_icons.png)

To change the pre-extrapolate and post-extrapolate modes, select the Animation clip and use the Animation Extrapolation properties in the Inspector window.

![Use Pre-Extrapolate and Post-Extrapolate to set the extrapolation modes for the selected Animation clip](../uploads/Main/timeline_inspector_anim_extrap.png) 

If the selected Animation clip is the only clip on the Animation track, you can set the Pre-Extrapolate mode to one of the following options:

* __None__: Turns off pre-extrapolation. In the gap before the selected Animation clip, the GameObject uses its transform, pose, or state from the scene. Selecting None is useful if, for example, you want to create an ease-in between the motion of a GameObject in the scene and an Animation clip. See [Easing-in and Easing-out Clips](TimelineEasingClips) for details.

* __Hold__ (default): In the gap before the selected Animation clip, the GameObject bound to the Animation track uses the values assigned at the start of the Animation clip.

* __Loop__: In the gap before the selected Animation clip, the GameObject bound to the Animation track repeats the entire animation as a forward loop: from start to end. Use the __Clip In__ property to offset the start of the loop. 

* __Ping Pong__: In the gap before the selected Animation clip, the GameObject bound to the Animation track repeats the entire animation forwards, then backwards. Use the __Clip In__ property to offset the start of the loop. Changing the __Clip In__ property affects the start of the loop, when looping forward, and the end of the loop, when looping backwards.

* __Continue__: In the gap before the selected Animation clip, the GameObject bound to the Animation track either holds or loops the animation based on the settings of the source asset. For example, if the selected Animation clip uses the motion file "Recorded(2)" as its source asset and "Recorded(2)" is set to loop, then selecting Continue loops the animation according to the "Recorded(2)" Loop Time settings.

If the selected Animation clip is the only clip on the Animation track, you can set the Post-Extrapolate mode to one of the following options:

* __None__: Turns off post-extrapolation. In the gap after the selected Animation clip, the GameObject uses its transform, pose, or state from the scene. Selecting None is useful if, for example, you want to create an ease-out between an Animation clip and the motion of a GameObject in the scene. See [Easing-in and Easing-out Clips](TimelineEasingClips) for details.

* __Hold__ (default): In the gap after the selected Animation clip, the GameObject bound to the Animation track uses the values assigned at the end of the Animation clip.

* __Loop__: In the gap after the selected Animation clip, the GameObject bound to the Animation track repeats the entire animation as a forward loop: from start to end. Use the __Clip In__ property to offset the start of the loop.

* __Ping Pong__: In the gap after the selected Animation clip, the GameObject bound to the Animation track repeats the entire animation forwards, then backwards. Use the __Clip In__ property to offset the start of the loop. Changing the __Clip In__ property affects the start of the loop, when looping forward, and the end of the loop, when looping backwards.

* __Continue__: In the gap after the selected Animation clip, the GameObject bound to the Animation track either holds or loops the animation based on the settings of the source asset. For example, if the selected Animation clip uses the motion file "Recorded(2)" as its source asset and "Recorded(2)" is set to loop, then selecting Continue loops the animation according to the "Recorded(2)" Loop Time settings.

When an Animation track contains a gap between two Animation clips, the __Post-Extrapolate__ setting of the left clip sets the gap extrapolation. If the __Post-Extrapolate__ setting of the clip to the left of a gap is set to None, the __Pre-Extrapolate__ setting of the right clip sets the gap extrapolation. Icons before and after Animation clips indicate whether the extrapolation for a gap is taken from the __Post-Extrapolate__ setting of the clip to the left or from the __Pre-Extrapolate__ setting of the clip to the right.

![First track (red): gap extrapolation from Post-Extrapolate of the left clip. Third track (blue): gap extrapolation from Pre-Extrapolate of the right clip.](../uploads/Main/timeline_gap_extrap_two_tracks.png)


---
* <span class="page-edit">2017-08-10  <!-- include IncludeTextNewPageSomeEdit --></span>