# Animation Track properties

Use the Inspector window to change the name of an Animation track, apply an avatar mask, apply track offsets, and to specify the transforms that are matched when matching clip offsets between Animation clips.

![Inspector window when selecting an Animation track in the Timeline Editor window](../uploads/Main/timeline_inspector_animation_track.png)

|**Property:** |**Function:** |
|:---|:---|
|__Display Name__| The name of the Animation track shown in the Timeline Editor window and in the Playable Director component. The Display Name applies to the Timeline Asset and all of its Timeline instances. You can only modify the Display Name by selecting the Animation track when editing a Timeline instance. |
|__Apply Avatar Mask__ | Use this property to enable Avatar masking. When enabled, the animation for all Animation clips on the track are applied based on the selected Avatar Mask. |
|&#160;&#160;&#160;&#160;_Avatar Mask_ | Use this property to select the Avatar Mask applied to all Animation clips on the Animation track. An Avatar Mask defines which humanoid body parts are animated by Animation clips on the selected Animation track. The body parts that are masked are animated by other Animation tracks in the Timeline Asset. For example, you can use an Avatar Mask to [combine the lower-body animation on an Animation track with the upper body animation on an Override Animation track](TimelineWorkflowOverrideMasking). |
|__Apply Track Offsets__ | Enable Apply Track Offsets to apply the same position and rotation offsets to all Animation clips, on the selected Animation track. There are two methods for applying a track offset: set the position and rotation offsets with gizmos in the Scene view, or specify the exact position and rotation track offset. |
|&#160;&#160;&#160;&#160;_Move tool_ | Enable the Move tool to show the Move Gizmo in the Scene view. Use the Move Gizmo to visually position the track offset. Positioning the Move Gizmo changes the Position properties. |
|&#160;&#160;&#160;&#160;_Rotate tool_ | Enable the Rotate tool to show the Rotate Gizmo in the Scene view. Use the Rotate Gizmo to visually rotate the track offset. Rotating the Rotate Gizmo changes the Rotation properties. |
|&#160;&#160;&#160;&#160;_Position_ | Use the Position properties to set the track offset in X, Y, and Z coordinates. |
|&#160;&#160;&#160;&#160;_Rotation_ | Use the Rotation properties to set the track rotation offset around the X, Y, and Z axes. |
|__Clip Offset Match Fields__ | Expand Clip Offset Match Fields to display a series of checkboxes that choose which transforms are matched when [matching clip offsets](TimelineMatchOffsets) between Animation clips. The Clip Offset Match Fields set the default matching options for all Animation clips on the same track. Use the [Animation Clip playable asset properties](TimelineAnimationClipPlayableProperties) to override these defaults for each Animation clip. |

---
* <span class="page-edit">2017-12-07  <!-- include IncludeTextNewPageSomeEdit --></span>
