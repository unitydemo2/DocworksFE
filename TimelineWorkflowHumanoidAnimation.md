# Creating humanoid animation

This workflow demonstrates how to use a Timeline Instance to animate a humanoid character with external motion clips. This workflow also demonstrates how to match clip offsets, manually adjust clip offsets, and create blends between clips to minimize jumping and sliding. Although this workflow uses a humanoid character, you can use this animation method for any GameObject.

This workflow assumes that you have already created a Timeline instance with an empty Animation track bound to a humanoid.

![For example, the Guard humanoid is bound to an empty Animation track](../uploads/Main/timeline_humanoid_start.png)

From your project, drag a motion clip into the Animation track to create a new Animation clip. For example, drag an idle pose as the first clip to start the humanoid from an idle position. Position and resize the idle clip as appropriate.

![Animation track, bound to the Guard humanoid, with an idle pose (Idle) as its Animation clip](../uploads/Main/timeline_humanoid_idle.png)

Add a second motion clip. In this example, a run and turn left clip (named Run_Left) is dragged onto the Animation track. Resize the Run_Left clip as appropriate. In this example, the Run_Left clip is resized to include one loop so that the Guard runs and turns 180 degrees.

![Animation track with an Idle clip and a Run_Left clip](../uploads/Main/timeline_humanoid_runleft.png)

Play the Timeline instance. Notice that the humanoid, Guard character, jumps between each Animation clip. This happens because the position of the humanoid character at the end of the first Animation clip (Idle) does not match the position at the start of the next Animation clip (Run_Left).

![The humanoid jumps between the first Animation clip, that ends at frame 29 (red arrow and box), and the second Animation clip, that starts at frame 30 (ghost with green arrow and box)](../uploads/Main/timeline_humanoid_before_match.png)

To fix the jump between clips, [match the offset of each Animation clip](TimelineMatchOffsets). The Timeline Editor window provides a few different methods for matching offsets. In this example, the second Animation clip is matched with the previous clip. To do this, select the Run_Left clip, Right-click and select Match Offsets to Previous Clip.

![Right-click and select Match Offsets to Previous Clip to match the offsets of the selected Animation clip with the preceding Animation clip](../uploads/Main/timeline_humanoid_match_menu.png)

![After matching offsets, the humanoid at the end of the first Animation clip (frame 29, red arrow) matches the position and rotation of the humanoid at the start of the second Animation clip (frame 30, ghost with green arrow)](../uploads/Main/timeline_humanoid_after_match.png)

Play the Timeline instance again. Although the position and rotation of the humanoid matches, there is still a jump between the two Animation clips because the humanoid is in different poses. At the end of the first Animation clip, the humanoid is standing upright with its feet together. At the start of the second Animation clip, the humanoid is bent forward with its feet apart.

Create a blend to remove the jump and transition between the two poses. Adjust the size of the clips, the Blend Area, the Clip In, and the shape of each Blend Curve to create a transition between the two poses. For example, in the transition between the Idle clip and the Run_Left clip, the Idle clip is changed to a duration of 36 and the Run_Left clip is repositioned to start at frame 25. The rest of the properties are left as their default values.

![Create a blend between the first two clips to create a smooth transition between the two animations](../uploads/Main/timeline_humanoid_blend.png)

As the Idle clip transitions to the Run_Left clip, the blend removes the obvious jump between poses and transitions between most body parts naturally. However, blending between the different positions of the foot results in an unnatural foot slide.

To fix foot sliding, you can manually adjust the root offset of an Animation clip so that the position of the foot changes less drastically, reducing the foot slide. To manually adjust the root offset, select the Animation clip in the Timeline Editor window. In the Inspector window, expand **Animation Playable Asset** and expand **Clip Root Motion Offsets**.

![Select an Animation clip. In the Inspector window, expand **Animation Playable Asset** (advanced properties) and expand **Clip Root Motion Offsets**.](../uploads/Main/timeline_inspector_animation_clip_playable.png)

The **Clip Root Motion Offsets**, both position and rotation, are not zero because performing Match Offsets to Previous Clip already set these values to match the root (hips) of the previous humanoid at the end of the previous Animation clip.

Under Clip Root Motion Offsets, enable the Move tool. The Move Gizmo appears in the Scene view, at the root of the Animation clip. Use one of the following methods to manual adjust the root offset position of the Animation clip:

* In the scene view, drag the Move Gizmo.

* In the Inspector window, change the value of the appropriate Position property.

![Enable the Move tool (Inspector window, blue arrow) to show the Move Gizmo (red arrow) in the Scene view. Use the Move Gizmo to manually position the root motion offset of the selected Animation clip.](../uploads/Main/timeline_humanoid_manual.png)

---
* <span class="page-edit">2017-12-07  <!-- include IncludeTextNewPageSomeEdit --></span>

