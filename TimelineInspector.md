# Timeline and the Inspector Window

The Inspector window displays information about the selected GameObject including all attached components and their properties. This section documents the properties in the Inspector window that appear when you select  one or many Timeline objects: a Timeline Asset, a track, or a clip.

If you select a single Timeline object, the Inspector window displays the properties for the selected object. For example, if you select an Animation clip, the Inspector window shows the [common properties](TimelineAnimationClipProperties) and [playable asset properties](TimelineAnimationClipPlayableProperties) for the selected Animation clip.

![Inspector window when selecting an Animation clip in the Timeline Editor window](../uploads/Main/timeline_inspector_animation_clip.png)

If you select multiple Timeline objects, and the selection includes Timeline objects with common properties, the Inspector window shows two sections: a section with properties that apply to the entire selection, and a section of common properties that apply to each selected object individually.

For example, if you select an Audio clip on one track and two Animation clips on another track, the Inspector window includes **Multiple Clip Timing** properties and **Clip Timing** properties:

* Use the **Multiple Clip Timing** properties to change the Start or End of the selection as a group. For example, if you change the Start to frame 30, the selection of clips start at frame 30. This moves the start of the first clip to frame 30 and the remaining selected clips are placed relative to the first clip, respecting gaps between selected clips.

* Use the **Clip Timing** properties to change the common properties for each selected clip individually. For example, if you change the Ease In Duration to 10 frames, the Ease In Duration of each selected clip changes to 10 frames. 

![Inspector window when selecting multiple clips, on multiple tracks, in the Timeline Editor window. If the selected clips have different values for a property, the value is represented with a dash ("-")](../uploads/Main/timeline_inspector_animation_clip.png)

If your selection includes Timeline objects that do not have common properties, the Inspector window prompts you to narrow the selection. For example, if you select an Animation track and an Audio clip in the Timeline Editor, you are prompted to narrow the selection. 

![If you select objects of different types, the Inspector window prompts you to narrow the selection to similar objects](../uploads/Main/timeline_inspector_narrow_selection.png)

---
* <span class="page-edit">2017-12-07  <!-- include IncludeTextAmendPageSomeEdit --></span>