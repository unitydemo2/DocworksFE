# Animation Clip playable asset properties

Use the Inspector window to change the playable asset properties of an Animation clip. The playable asset properties include controls for manually transforming the root motion offset of the Animation clip and options for overriding default clip matching. 

To view the playable asset Animation Clip properties, select an Animation clip in the Timeline Editor window and expand **Animation Playable Asset** in the Inspector window.

![Inspector window showing the playable asset properties of the selected Animation clip](../uploads/Main/timeline_inspector_animation_clip_playable.png)

## Clip Root Motion Offsets

Use the **Clip Root Motion Offsets** to apply position and rotation offsets to the root motion of the selected Animation clip. There are two methods of applying clip root offsets: 

* [Match the clip offsets](TimelineMatchOffsets) to set the root motion offsets based on the end of the previous Animation clip, or the start of the next Animation clip. What gets matched depends on the **Clip Offset Match Fields**.

* Use the tools and properties under **Clip Root Motion Offsets** to manually set the position and rotation of the root motion offsets. 

|**Property:** |**Function:** |
|:---|:---|
|__Move tool__| Enable the Move tool to show a Move Gizmo in the Scene view. Use the Move Gizmo to manually position the root motion offset for the selected Animation clip. Using the Move Gizmo changes the Position properties. |
|__Rotate tool__ | Enable the Rotate tool to show a Rotate Gizmo in the Scene view. Use the Rotate Gizmo to manually rotate the root motion offset for the selected Animation clip. Using the Rotate Gizmo changes the Rotation properties. |
|__Position__ | Use the Position properties to manually set the clip offset in X, Y, and Z coordinates. By default, the Position coordinates are set to zero and are relative to the [track offsets](TimelineAnimationTrackProperties). |
|__Rotation__ | Use the Rotation properties to manually set the clip rotation offset around the X, Y, and Z axes. By default, the Rotation coordinates are set to zero and are relative to the [track offsets](TimelineAnimationTrackProperties). |

## Clip Offset Match Fields

Use the **Clip Offset Match Fields** to choose which transforms are matched when [matching clip offsets](TimelineMatchOffsets). By default, **Override Track Match Fields** is disabled and the **Clip Offset Match Fields** show and use the matching options set at the [Animation track level](TimelineAnimationTrackProperties).

Enable **Override Track Match Fields** to override the track match options and set which transformations are matched for the selected Animation clip.

---
* <span class="page-edit">2017-12-07  <!-- include IncludeTextNewPageSomeEdit --></span>

