# Timeline Editor window

To access the Timeline Editor window, select __Timeline Editor__ from the Window menu. What the Timeline Editor window shows depends on what you select in either the Project window or the Scene view. 

For example, If you select a GameObject that is associated with a Timeline Asset, the Timeline Editor window shows the tracks and clips from the Timeline Asset and the GameObject bindings from the Timeline instance.

![Selecting a GameObject associated with a Timeline Asset displays its tracks, its clips, and the bindings from the TImeline instance](../uploads/Main/timeline_editor_bindings.png)

If you haven’t selected a GameObject, the Timeline Editor window informs you that the first step for creating a Timeline Asset and a Timeline instance is to select a GameObject.

![With no GameObject selected, the Timeline Editor window provides instructions](../uploads/Main/timeline_editor_to_start.png)

If a GameObject is selected and it is not associated with a Timeline Asset, the Timeline Editor window provides the option for creating a new Timeline Asset, adding the necessary components to the selected GameObject, and creating a Timeline instance.

![Select a GameObject that is not associated with a Timeline Asset to create a new Timeline Asset, add components, and create a Timeline instance.](../uploads/Main/timeline_editor_create.png)

To use the Timeline Editor window to view a previously created Timeline Asset, select the Timeline Asset in the Project window and open the Timeline Editor window.  The Timeline Editor window shows the tracks and clips associated with the Timeline Asset, but without the track bindings to GameObjects in the scene. In addition, the Timeline Playback Controls are disabled and there is no Timeline Playhead.

![Timeline Asset selected in the Project window shows its tracks and clips but with no track bindings, Timeline Playback Controls, or Timeline Playhead](../uploads/Main/timeline_editor_project.png) 

The track bindings to GameObjects in the scene are not saved with the Timeline Asset. The track bindings are saved with the Timeline instance. For details on the relationship between the project, the scene, Timeline Assets, and Timeline instances, see [Timeline overview](TimelineOverview).

---
* <span class="page-edit">2017-08-10  <!-- include IncludeTextNewPageSomeEdit --></span>