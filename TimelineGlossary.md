# Timeline glossary

This section provides an alphabetical list of the terminology used throughout the Timeline documentation.

__animatable property__: A property belonging to a GameObject, or belonging to a component added to a GameObject, that can have different values over time.

__animation__: The result of adding two different keys, at two different times, for the same animatable property. 

__animation curve__: The curve drawn between keys set for the same animatable property, at different frames or seconds. The position of the tangents and the selected interpolation mode for each key determines the shape of the animation curve. 

__binding__ or __Track binding__: Refers to the link between Timeline Asset tracks and the GameObjects in the scene. When you link a GameObject to a track, the track animates the GameObject. Bindings are stored as part of the Timeline instance.

__blend__ and __blend area__: The area where two Animation clips, Audio clips, or Control clips overlap. The overlap creates a transition that is referred to as a __blend__. The duration of the overlap is referred to as the __blend area__. The blend area sets the duration of the transition.

__Blend In curve__: In a blend between two Animation clips, Audio clips, or Control clips, there are two blend curves. The blend curve for the incoming clip is referred to as the __Blend In__ curve. 

__Blend Out curve: __In a blend between two Animation clips, Audio clips, or Control clips, there are two blend curves. The blend curve for the out-going clip is referred to as the __Blend Out__ __curve__. 

__clip__: A generic term that refers to any clip within the Clips view of the Timeline Editor window. 

__Clips view__: The area in the Timeline Editor window where you add, position, and manipulate clips. 

__Control/Command__: This term is used when instructing the user to press or hold down the Control key on Windows, or the Command key on Mac. 

__Curves view__: The area in the Timeline Editor window that shows the animation curves for Infinite clips or for Animation clips that have been converted from Infinite clips. The Curves view is similar to [Curves mode](animeditor-AnimationCurves) in the Animation window.

__Gap extrapolation__: How an Animation track approximates animation data in the gaps before and after an Animation clip. 

__field__: A generic term that describes an editable box that the user clicks and types-in a value. A field is also referred to as a __property__.

__incoming clip:__ The second clip in a blend between two clips. The first clip, the out-going clip, transitions to the second clip, the __incoming clip__.

__infinite clip__: A special animation clip that contains basic key animation recorded directly to an Animation track within the Timeline Editor window. An Infinite clip cannot be positioned, trimmed, or split because it does not have a defined duration: it spans the entirety of an Animation track.

__interpolation__: The estimation of values that determine the shape of an animation curve between two keys. 

__interpolation mode__: The interpolation algorithm that draws the animation curve between two keys. The interpolation mode also joins or breaks left and right tangents.

__key__: The value of an animatable property, set at a specific point in time. Setting at least two keys for the same property creates an animation.

__out-going clip__: The first clip in a blend between two clips. The first clip, the __out-going clip__, transitions to the second clip, the incoming clip. 

__Playhead Location field__: The field that expresses the location of the Timeline Playhead in either frames or seconds, depending on the Timeline Settings.

__property__: A generic term for the editable fields, buttons, checkboxes, or menus that comprise a component. An editable field is also referred to as a __field__.

__tangent__: One of two handles that controls the shape of the animation curve before and after a key. Tangents appear when a key is selected in the Curves view, or when a key is selected in the Curve Editor.

__tangent mode__: The selected interpolation mode used by the left tangent, right tangent, or both tangents.

__Timeline__ or __Unity's Timeline__: Generic terms that refer to all features, windows, editors, and components related to creating, modifying, or reusing cut-scenes, cinematics, and game-play sequences.

__Timeline Asset__: Refers to the tracks, clips, and recorded animation that comprise a cinematic, cut-scene, game-play sequence, or other effect created with the Timeline Editor window. A Timeline Asset does not include bindings to the GameObjects animated by the Timeline Asset. The bindings to scene GameObjects are stored in the Timeline instance. The Timeline Asset is project-based.

__Timeline Editor window__: The official name of the window where you create, modify, and preview a Timeline instance. Modifications to a Timeline instance also affects the Timeline Asset.

__Timeline instance__: Refers to the link between a Timeline Asset and the GameObjects that the Timeline Asset animates in the scene. You create a Timeline instance by associating a Timeline Asset to a GameObject through a Playable Director component. The Timeline instance is scene-based.

__Timeline Playback Controls__: The row of buttons and fields in the Timeline Editor window that controls playback of the Timeline instance. The Timeline Playback Controls affect the location of the Timeline Playhead.

__Timeline Playback mode__: The mode that previews the Timeline instance in the Timeline Editor window. Timeline Playback mode is a simulation of Play mode. Timeline Playback mode does not support audio playback.

__Timeline Playhead__: The white marker and line that indicates the exact point in time being previewed in the Timeline Editor window.

__Timeline Selector__: The name of the menu in the Timeline Editor window that selects the Timeline instance to be previewed or modified.

__track__: A generic term that refers to any track within the Track list of the Timeline Editor window.

__Track groups__: The term for a series of tracks organized in an expandable and collapse collection of tracks. 

__Track list__: The area in the Timeline Editor window where you add, group, and modify tracks.


---
* <span class="page-edit">2017-08-10  <!-- include IncludeTextNewPageSomeEdit --></span>
