# Playable Director component

The Playable Director component stores the link between a Timeline instance and a Timeline Asset. The Playable Director component controls when the Timeline instance plays, how the Timeline instance updates its clock, and what happens when the Timeline instance finishes playing. 

![Playable Director component added to the GameObject named PickupObject. The GameObject is associated with the PickupTimeline Timeline Asset.](../uploads/Main/timeline_inspector_playable_director.png)

The Playable Director component also shows the list of tracks, from the associated Timeline Asset (__Playable__ property), that animate GameObjects in the scene. The link between Timeline Asset tracks and GameObjects in the scene is referred to as __binding__ or __Track binding__. See [Timeline Overview section](TimelineOverview) for details on binding and the relationship between Timeline Assets and Timeline instances.

### Playable

Use the __Playable__ property to manually associate a Timeline Asset with a GameObject in the scene. When you make this association, you create a Timeline instance for the selected Timeline Asset. After you create a Timeline instance, you can use the other properties in the Playable Director component to control the instance and to choose which GameObjects in the scene are animated by the Timeline Asset.

### Update Method

Use the Update Method to set the clock source that the Timeline instance uses to update its timing. The Update Method supports the following clock sources:

* __DSP__: Select for sample accurate audio scheduling. When selected, the Timeline instance uses the same clock source that processes audio. DSP stands for digital signal processing.

* __Game Time__: Select to use the same clock source as the game clock. This clock source is affected by [time scaling](TimeFrameManagement).

* __Unscaled Game Time__: Select to use the same clock source as the game clock, but without being affected by time scaling.

* __Manual__: Select to not use a clock source and to manually set the clock time through scripting.

### Play on Awake

Whether the Timeline instance is played when game play is initiated. By default, a Timeline instance is set to begin as soon as the scene begins playback. To disable the default behaviour, disable the Play on Awake option in the Playable Director component. 

### Wrap Mode

The behaviour when the Timeline instance ends playback. The Wrap mode also defines the behaviour when the Timeline Editor window is in Play Range mode. The following Wrap modes are supported:

* __Hold__: Plays the Timeline instance once and holds on the last frame until playback is interrupted.

* __Loop__: Plays the sequence repeatedly until playback is interrupted.

* __None__: Plays the sequence once and then resets all animated properties to the values they held before playback.

### Initial Time

The time (in seconds) at which the Timeline instance begins playing. The Initial Time adds a delay in seconds from when the Timeline instance is triggered to when playback actually begins. For example, if Play On Awake is enabled and Initial Time is set to five seconds, clicking the Play button in the Unity Toolbar starts Play mode and the Timeline instance begins at five seconds.

This is useful when you are working on a long cinematic and you want to preview the last few seconds of your Timeline instance. 

### Current Time

Use the Current Time field to view the progression of time according to the Timeline instance in the Timeline Editor window. The Current Time field matches the Playhead Location field. The Current Time field is useful when the Timeline Editor window is hidden. The Current Time field appears in the Playable Director Component when in Timeline Playback mode or when Unity is in Game Mode.

### Bindings

Use the __Bindings__ area to link GameObjects in the scene with tracks from the associated Timeline Asset (__Playable__ property). When you link a GameObject to a track, the track animates the GameObject in the scene. The link between a GameObject and a track is referred to as __binding__ or __Track binding__. 

The __Bindings__ area is split into two columns:

* The first column lists the tracks from the Timeline Asset. Each track is identified by an icon and its track type. 

* The second column lists the GameObject linked (or __bound__) to each track.

The __Bindings__ area does not list Track groups, Track sub-groups, or tracks that do not animate GameObjects. The Timeline Editor window shows the same bindings in the [Track list](TimelineTrackList).


---
* <span class="page-edit">2017-08-10  <!-- include IncludeTextNewPageSomeEdit --></span>