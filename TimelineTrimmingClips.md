### Trimming clips

Drag the start or end of a clip to trim its duration. Dragging the start or end of a clip automatically selects the clip, showing its properties in the Inspector window. Use the [Clip Timing properties](script-EditorClip) in the Inspector window to set the start, end, duration, and offset (Clip In) of a clip to exact values.

![Position and trim a clip by adjusting its Start, End, Duration, and Clip In properties in the Inspector window](../uploads/Main/timeline_inspector_clip_timing.png)

#### Trimming the start of a clip

When trimming the start of an Animation clip or Audio clip in the Clips view, the start cannot be dragged before the start of the source asset that the clip is based on. Trimming an Animation clip or Audio clip after the start of the source asset selects the section of the source asset used by the clip.

![Trimming the start of an Animation clip selects the section of key animation used by the clip](../uploads/Main/timeline_clip_trim_start_keys.png)

Trimming a clip is non-destructive. Trim the clip again to modify its start to include the animation, or the audio waveform, cut off during a previous trim. You can also [reset a clip](TimelineResettingClips) to undo trims or other edits.

To trim the start of a clip to a precise time or frame, use the __Clip In__ property in the Inspector window. Changing the __Clip In__ property has the same effect as trimming the start of a clip after the start of its source asset.

#### Trimming the end of a clip

As with the start of the clip, trimming an Animation clip or Audio clip before the end of the source asset, trims the part of the source asset used by the clip.

![Trimming the end of an Animation clip trims its key animation](../uploads/Main/timeline_clip_trim_end_keys.png)

If you trim the end of an Animation clip or Audio clip past the end of the source asset the clip is based on, the extra clip area either holds or loops, depending on the settings of the source asset.

For example, an Animation clip named "End Move" uses the motion file "Recorded(2)" as its source asset. The motion file "Recorded(2)" is set to loop. Trimming the end of the Animation clip past the end of the "Recorded(2)" source asset fills the extra clip area by looping "Recorded(2)". A white animation curve shows the hold or loop.

![A white animation curve indicates whether the extra clip area holds or loops data, depending on the source asset](../uploads/Main/timeline_clip_trim_loop.png)

To choose whether the extra clip area holds or loops, select the source asset to change its settings in the Inspector window. Depending on the type of source asset, different properties control whether the source asset holds or loops.

If you are unsure which source asset is used by a clip, select the clip in the Clips view, Right-click and select __Find Source Asset__ from the context menu. This highlights the source asset in the Project window. 

#### Trimming the end of looping clips

The Timeline Editor window provides special trimming options for Animation clips or Audio clips with loops. These special trim options either remove the last partial loop or complete the last partial loop.

For example, the Animation clip named run_away is over three times longer than the source asset on which it is based. Since the source asset is set to loop, the Animation clip loops the source asset until the Animation clip ends which results in a partial loop.

![L1, L2, and L3 signify complete loops. The clip ends partially through the fourth loop, L4.](../uploads/Main/timeline_last_loop_before.png) 

To extend the end of the clip and complete a partial loop, select the clip, Right-click and select __Editing__ > __Complete Last Loop__. To trim the clip at the last complete loop, select the clip, Right-clip and select __Editing__ > __Trim Last Loop__.

![The result of select Editing > Complete Last Loop](../uploads/Main/timeline_last_loop_complete.png)

![The result of select Editing > Trim Last Loop](../uploads/Main/timeline_last_loop_trim.png)

#### Trimming with the Timeline Playhead

You can also trim a clip based on the location of the playhead. To trim using the playhead, position the playhead within the clip to be trimmed. Right-click the clip and select either __Editing__ > __Trim Start__ or __Editing__ > __Trim End__. __Trim Start__ trims the start of the clip to the playhead. __Trim End__ trims the end of the clip to the playhead.

![Move the Timeline Playhead within the clip](../uploads/Main/timeline_playhead_trim_before.png)

![Right-click and select Editing > Trim Start to trim the start of the clip to the playhead](../uploads/Main/timeline_playhead_trim_after.png)

If you select clips on multiple tracks, only the selected clips that intersect the playhead are trimmed.

---
* <span class="page-edit">2017-08-10  <!-- include IncludeTextNewPageSomeEdit --></span>
