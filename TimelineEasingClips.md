### Easing-in and Easing-out clips

Ease-in and ease-out a clip to create a smooth transition between a clip and its surrounding gaps. To create an ease-in or ease-out transition, use one of the following methods:

* Hold Control/Command and drag the start of a clip to the right to add an ease-in.

* Hold Control/Command and drag the end of a clip to the left to add an ease-out.

* Select the clip and, in the Inspector window, set either the __Ease In Duration__ or the __Ease Out Duration__.

![Ease-in and ease-out an Animation clip to transition between its animation and its gaps. All ease-in and ease-out transitions are represented by a linear curve.](../uploads/Main/timeline_clip_ease_in_out.png)

What an ease-in or ease-out transition effects differs depending on the track:

* On an Animation track or an Animation Override track, ease-in an Animation clip to create a smooth transition between the animation in the gap before the clip and the Animation clip. Ease-out an Animation clip to create a smooth transition between the Animation clip and the animation in the gap after the clip. There are many factors that determine what animation occurs in the gap before and after an Animation clip. See [Setting gap extrapolation](TimelineGapExtrapolation) for details.

* On an Audio track, ease-in an Audio clip to fade in the volume of the audio waveform. Ease-out an Audio clip to fade out the volume of the audio waveform specified by the Audio clip.

* On a Playable track, ease-In a Playable clip to fade in the effect or script in the Playable clip. Ease-Out a Playable clip to fade out the effect or script in the Playable clip.

Although the Clips view represents an ease-in or ease-out as a single linear curve, every ease-in or ease-out transition is actually set to a gradually easing-in or easing-out curve by default. To change the shape of either the ease-in curve (labelled In) or the ease-out (labelled Out) curve, use the Blend Curves in the Inspector window. 

![Use the Blend Curves to customize ease-in or ease-out transitions](../uploads/Main/timeline_inspector_blend_curves.png)

Note that the __Blend Curves__ might affect the blend area used for blending between two clips. The __Ease In Duration__ and __Ease Out Duration__ properties indicate whether the __Blend Curves__ affect an ease-in, an ease-out, or a blend. For example, If the __Ease Out Duration__ is editable, then the Blend Out curve (labelled __Out__) affects the curve used by an ease-out transition. If the __Ease Out Duration__ cannot be edited, then the Blend Out curve (labelled __Out__) affects the out-going clip in a blend between two clips.

![Ease Out Duration cannot be edited, therefore the Out curve affects the blend area between two clips](../uploads/Main/timeline_inspector_ease_in_blend_out.png)

To customize either the ease-in or ease-out transition, use the drop-down menu to switch from __Auto__ to __Manual__. With __Manual__ selected, the Inspector window shows a preview of the blend curve. Click the preview to open the Curve Editor below the Inspector window.

![Select Manual and click the preview to open the Curve Editor](../uploads/Main/timeline_inspector_curve_editor.png)

The Curve Editor is the same editor that is used to customize the shape of the blend curves when [blending between clips](TimelineBlendingClips).

When creating an ease-in or an ease-out with Animation clips, the Animation clip blends between its gaps and the Animation clip. The following factors affect the values of animated properties in the gaps surrounding an Animation clip:

* The [pre-extrapolate and post-extrapolate settings](TimelineGapExtrapolation) for the Animation clip and for other Animation clips on the same track.

* Animation clips on other Animation tracks that are bound to the same GameObject.

* The position or animation of the GameObject in the scene, outside the Timeline Asset.

#### Gap extrapolation and easing clips

To successfully ease-in or ease-out an Animation clip, the gap extrapolation must not be set based on the Animation clip being eased-in or eased-out. The gap extrapolation must either be set to None or it must be set by other Animation clip.

For example, the following ease-in has no effect because the Pre-Extrapolate for the Victory_Dance clip is set to Hold. This means that the ease-in creates a transition between the first frame of the Animation clip and the rest of the Animation clip.

![The gap is set to Hold from the Animation clip (circled). The ease-in has no effect.](../uploads/Main/timeline_clip_ease_in_bad_gap.png)

![To ease-in from the Idle clip, set pre-extrapolate for the Victory_Dance clip to None. The ease-in gap uses the post-extrapolate mode from the Idle clip (circled).](../uploads/Main/timeline_clip_ease_in_good_gap.png)

#### Overriding Animation tracks with ease-in and ease-out

If the gap extrapolation is set to None, and there is a previous track bound to the same GameObject, the animation in the gap is taken from the previous track. This is useful for creating a smooth transition between two Animation clips on different tracks. 

For example, if two Animation tracks are bound to the same GameObject and a clip on the second track contains an ease-in, the ease-in creates a smooth transition between the animation on the previous track and the animation on the second track. To successfully override animation on a previous track, the gap extrapolation for the second track must be set to None.

![The Animation clip on the first track is a repeated idle cycle where the humanoid GameObject stands still. The Animation clip in the second track eases-in the Victory_Dance motion and ease-out to return back to the idle cycle.](../uploads/Main/timeline_clip_ease_in_override_track.png)

#### Overriding the scene with ease-in and ease-out

In the scene, if a GameObject is controlled with an Animator Controller, you can use an ease-in or ease-out transition between the Animation clip and the Animator Controller. 

For example, if a Timeline Asset contains a single track with a single Animation clip and all its gap extrapolation settings are set to None, the gap uses the position or animation of the GameObject from the scene. 

This position or animation is the GameObject as set in the scene. If the GameObject uses an Animator Controller to control its animation state, the gap is set to the current animation state. For example, if the GameObject is a character walking in the scene, a Timeline Asset could be setup to ease-in animation to override the walking animation state. The ease-out returns the GameObject to the animation state according to the Animator Controller.

![A single Animation clip with all gap extrapolation set to None eases-in and ease-out the GameObject between its position or animation in the scene and the Animation clip](../uploads/Main/timeline_clip_ease_in_override_scene.png)

---
* <span class="page-edit">2017-08-10  <!-- include IncludeTextNewPageSomeEdit --></span>