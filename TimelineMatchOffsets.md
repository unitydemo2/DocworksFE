# Matching clip offsets

Every Animation clip contains key animation, or motion, that animates the GameObject, or humanoid, bound to the Animation track. When you add an Animation clip to an Animation track, its key animation or motion does not automatically match the previous clip or the next clip on the Animation track. By default, each Animation clip begins at the position and rotation of the GameObject, or humanoid, at the beginning of the Timeline instance.

![For example, three Animation clips create an animation sequence that starts with a clip of a humanoid standing and running, continues with a clip of the humanoid running while turning left, and ends with the humanoid running and standing still](../uploads/Main/timeline_match_prematch_clips.png)

![Each Animation clip begins at the position and rotation of the humanoid at the start of the Timeline instance (red arrow). The three Animation clips, Stand2Run, RunLeft, and Run2Stand, all begin at the red arrow but end at the green, blue, and yellow arrows, respectively.](../uploads/Main/timeline_match_prematch_scene.png)

For an animation sequence to flow seamlessly between adjacent Animation clips, you must match each Animation clip with its previous or next clip. Matching clips adds a position and rotation offset for each Animation clip, referred to as the Clip Root Motion Offset. The following sections describe how to match two Animation clips or many Animation clips.

## Matching two clips

To match the root motion between two clips, RIght-click the Animation clip that you want to match. From the context menu, select either Match Offsets to Previous Clip or Match Offsets to Next Clip.

![For example, Right-click the middle Animation clip, named "RunLeft", to match its offsets to either the previous clip or the next clip](../uploads/Main/timeline_match_clip_two.png)

The context menu only displays the Match Offset options available for the clicked Animation clip. For example, if there is a gap **before** the clicked Animation clip, only the Match Offsets to Next Clip menu item is available.

When you are matching offsets for a single Animation clip, it is not necessary to select the Animation clip first, but you must Right-click the Animation clip that you want to match. For example, if you Right-click on an Animation clip that is not selected, the clicked clip is matched and any selected Animation clips are ignored.

## Matching many clips

To match the root motion of many clips, select the Animation clips that you want to match and RIght-click on one of the selected clips. From the context menu, select either Match Offsets to Previous Clip or Match Offsets to Next Clip.

![For example, select the "RunLeft" and "Run2Stand" clips. Right-click one of the selected clips, and select Match Offsets to Previous Clips, to match the RunLeft clip with the previous clip Stand2Run, and to match Run2Stand with the previous clip RunLeft.](../uploads/Main/timeline_match_clip_many.png)

---
* <span class="page-edit">2017-12-07  <!-- include IncludeTextNewPageNoEdit --></span>

