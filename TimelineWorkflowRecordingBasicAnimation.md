## Recording basic animation with an Infinite clip

You can record animation directly to an Animation track. When you record directly to an empty Animation track, you create an __Infinite clip__.

An Infinite clip is defined as a clip that contains basic key animation recorded through the Timeline Editor window. An Infinite clip cannot be positioned, trimmed, or split because it does not have a defined size: it spans the entirety of an Animation track. 

Before creating an Infinite clip, you must [add an empty Animation track](TimelineAddingTracks) for the GameObject that you want to animate.

In the Track list, click the Record button for the empty Animation track to enable Record mode. The Record button is available for Animation tracks bound to simple GameObjects such as cubes, spheres, lights, and so on. The Record button is disabled for Animation tracks bound to humanoid GameObjects.

![Click the Record button on an empty track to enable Record mode](../uploads/Main/timeline_workflow_record_button.png) 

When a track is in Record mode, the clip area of the track is drawn in red with the "Recording..." message. The Record button blinks.

![Timeline Editor window in Record mode](../uploads/Main/timeline_workflow_recording.png)

When in Record mode, any modification to an animatable property of the GameObject sets a key at the location of the Timeline Playhead. Animatable properties include transforms and the animatable properties for all components added to the GameObject.

To start creating an animation, move the Timeline Playhead to the location of the first key, and do one of the following: 

* In the Inspector window, Right-click the name of the property and choose __Add Key__. This adds an animation key for the property without changing its value. A white diamond appears in the infinite clip to show the position of the key.

* In the Inspector window, change the value of the animatable property of the GameObject. This adds an animation key for the property with its changed value. A white diamond appears in the infinite clip.

* In the Scene view, move, rotate, or scale the GameObject to add a key. This automatically adds a key for the properties you change. A white diamond appears in the infinite clip.

![Red background indicates that an animation curve for the property has been added to the clip](../uploads/Main/timeline_property_red.png)

![Setting a key adds a white diamond to the infinite clip](../uploads/Main/timeline_workflow_recording_diamonds.png)

Move the playhead to a different position on the timeline and change the animatable properties of the GameObject. At each position, the Timeline Editor window adds a white diamond to the Infinite clip for any changed properties and adds a key to its associated animation curves. 

While in Record mode, you can Right-click the name of an animatable property name to perform keying operations such as setting a key without changing its value, jumping to the next or previous keys, removing keys, and so on. For example, to set a key for the position of a GameObject without changing its value, Right-click __Position__ and select __Add Key__ from the context menu.

![Right-click the name of an animatable property to perform keying operations](../uploads/Main/timeline_workflow_keyframing_menu.png) 

When you finish the animation, click the blinking Record button to disable Record mode.

An Infinite clip appears as a dopesheet in the Timeline Editor window, but you cannot edit the keys in this view. Use [the Curves view to edit keys](TimelineEditingKeys). You can also Double-click the Infinite clip and edit the keys with the Animation window. 

![An Infinite clip appear as a dopesheet](../uploads/Main/timeline_workflow_dopesheet.png)

Save the scene or project to save the Timeline Asset and the Infinite clip. The Timeline Editor window saves the key animation from the Infinite clip as a source asset. The source asset is named "Recorded" and saved as a child of the Timeline Asset in the project. 

![Recorded clips are saved under the Timeline Asset in the project](../uploads/Main/timeline_workflow_clip_in_project.png)

For every additional recorded Infinite clip, each clip is sequentially numbered starting at "(1)". For example, a Timeline Asset with three recorded Infinite clips are named "Recorded", "Recorded (1)", and "Recorded (2)". If you delete a Timeline Asset, its child clips are also removed.

---
* <span class="page-edit">2017-08-10  <!-- include IncludeTextNewPageSomeEdit --></span>