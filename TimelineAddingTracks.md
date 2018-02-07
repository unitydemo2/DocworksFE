### Adding tracks

The Timeline Editor window supports many different methods of adding tracks to the Track list. The method you choose impacts GameObjects, Track binding, and components. 

The simplest method of adding a track is to click the Add button and select the type of track from the Add Track menu. You can also Right-click in an empty area of the Track list and select the type of track from the Add Track menu.

![Add Track menu](../uploads/Main/timeline_add_track_menu.png)

The Timeline Editor window also supports dragging a GameObject into the Track list. Drag a GameObject into an empty area in the Track list and select the type of track to add from the context menu. Depending on the type of track selected, the Timeline Editor window performs different actions:

* Select Animation Track and the Timeline Editor binds the GameObject to the Animation track. If the GameObject doesn't already have an Animator component, the Timeline Editor creates an Animator component for the GameObject.

* Select Activation Track and the Timeline Editor binds the GameObject to the Activation track. There are some limitations when creating an Activation track when dragging a GameObject. For example, the main GameObject with the Playable Directory component should not be bound to an Activation track. Since this is the same GameObject that links the Timeline Asset to the scene, activating and disabling the GameObject affects the length of Timeline instance.

* Select Audio Track and the Timeline Editor adds an Audio Source component to the GameObject and binds this Audio Source component to the Audio Track.

---
* <span class="page-edit">2017-08-10  <!-- include IncludeTextNewPageSomeEdit --></span>