# Using Animation Override Tracks and Avatar Masking

This workflow demonstrates how to use an Animation Override track and an Avatar Mask to replace the upper-body animation of an Animation track. Use this technique to animate a humanoid character to, for example, run and carry an object.

This workflow **does not** show how to [create an Avatar mask](class-AvatarMask). This workflow only demonstrates how to use an Avatar Mask when creating a Timeline instance. This workflow also assumes that you have already created a Timeline instance with a simple Animation clip, such as a walk or run cycle, on an Animation track bound to a humanoid.

![The Guard humanoid is bound to an Animation track with a run cycle (Run_Forward) that loops once](../uploads/Main/timeline_masking_start.png)

Right-click the Animation track and select Add Override Track from the context menu. An Animation Override track, named Override 0, is linked to the selected Animation track. Notice that the Animation Override track is not bound to a GameObject. Since the Override track is linked to the Animation track above, the Override track is bound to the same GameObject: the Guard humanoid.

![Add an Override track. Right-click the Animation track and select Add Override Track from the context menu.](../uploads/Main/timeline_masking_override.png)

From your project, drag an animation clip with upper-body animation into the Override track. For example, drag an animation of a humanoid standing still and waving their arms. Position and resize the Waving_Arms clip as appropriate.

![The Animation Override track contains an Animation clip of a humanoid standing still, waving their arms. The clip is resized to match the Animation clip (Run_Forward) of the parent Animation track.](../uploads/Main/timeline_masking_waving.png)

Play the Timeline instance. The Waving_Arms clip completely overrides the Run_Forward clip. To combine the lower-body animation from the Run_Forward clip with the upper-body animation from the Waving_Arms clip, specify an Avatar Mask for the Animation Override track.

![To specify an Avatar Mask, select the Override track to view its properties in the Inspector window](../uploads/Main/timeline_masking_override_selected.png)

From the project, drag an Avatar Mask into the Avatar Mask property in the Inspector window. Activate the Apply Avatar Mask checkbox. An Avatar Mask icon appears beside the track name.

![An Avatar Mask, that masks the upper-body animation, is specified for the Animation Overview clip in the Inspector window.](../uploads/Main/timeline_masking_avatar_inspector.png)

![The Avatar Mask icon (red circle) indicates that the Animation track uses an Avatar Mask. Select and activate the Avatar Mask in the Inspector window.](../uploads/Main/timeline_masking_avatar_on.png)

Play the Timeline instance. On the Guard humanoid, the upper-body animation is taken from the Waving_Arms clip and the lower-body animation is from the Run_Forward clip. To temporarily disable the Avatar Mask, click the Avatar Mask icon.

![The Avatar Mask icon (red circle) disappears when disabled. The Waving_Arms animation completely overrides the Run_Forward animation.](../uploads/Main/timeline_masking_avatar_off.png)

---
* <span class="page-edit">2017-12-07  <!-- include IncludeTextNewPageSomeEdit --></span>
