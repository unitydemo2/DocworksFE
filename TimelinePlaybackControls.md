## Timeline Playback Controls

Use the buttons and fields in the Timeline Playback Controls to play the Timeline instance and to control the location of the Timeline Playhead.

![Timeline Playback Controls](../uploads/Main/timeline_playback_controls.png)

### Timeline Start button

![](../uploads/Main/timeline_start_button.png)

Click the Timeline Start button, or hold Shift and press Comma (,), to move the Timeline Playhead to the start of the Timeline instance.

### Previous Frame button

![](../uploads/Main/timeline_previous_frame_button.png)

Click the Previous Frame button, or press Comma (,), to move the Timeline Playhead to the previous frame.

### Timeline Play button

![](../uploads/Main/timeline_play_button.png)

Click the Timeline Play button, or press the Spacebar, to preview the Timeline instance in Timeline Playback mode. Timeline Playback mode does the following:

* Begins playback at the current location of the Timeline Playhead and continues to the end of the Timeline instance. If the Play Range button is enabled, playback is restricted to a specified time range.

* The Timeline Playhead position moves along the Timeline instance. The Playhead Location field shows the position of the Timeline Playhead in either frames or seconds, depending on the [Timeline settings](TimelineSettings). 

* To pause playback, click the Timeline Play button again, or press the Spacebar. 

* When playback reaches the end of the Timeline instance, the Wrap Mode determines whether playback should hold, repeat, or do nothing. The Wrap Mode setting is a property of the the [Playable Director component](class-PlayableDirector).

Timeline Playback mode provides a preview of the Timeline instance while in the Timeline Editor window. Timeline Playback mode is only a simulation of Game Mode that does not support audio playback. To preview a Timeline instance with audio, you can enable the Play on Awake option in the Playback Director component and preview game play by using the Play mode.

### Next Frame button

![](../uploads/Main/timeline_next_frame_button.png)

Click the Next Frame button, or press Period (.), to move the Timeline Playhead to the next frame.

### Timeline End button

![](../uploads/Main/timeline_end_button.png)

Click the Timeline End button, or hold Shift and press Period (,), to move the Timeline Playhead to the end of the timeline.

### Play Range button

![](../uploads/Main/timeline_play_range_button.png)

Enable the Play Range button to restrict playback to a specific range of seconds or frames. The timeline highlights the play range and indicates its start and end with white markers. To modify the play range, drag either marker.

![Play Range enabled with while markers defining range](../uploads/Main/timeline_play_range.png)

The __Wrap Mode__ property of the [Playable Director component](class-PlayableDirector) determines what happens when playback reaches the end marker.

You can only set a play range when previewing a Timeline instance within the Timeline Editor window. Unity ignores the play range in Play mode.

### The Playhead Location field and Timeline Playhead

The Timeline Playhead indicates the exact point in time being previewed in the Timeline Editor window. The Playhead Location field expresses the location of the Timeline Playhead in either frames or seconds. 

![Playhead Location field and Timeline Playhead](../uploads/Main/timeline_playhead_location.png)

To jump the Timeline Playhead to a specific time, click the timeline. You can also enter the time value in the Playhead Location field and press Enter. When typing a value, frames are converted to seconds or seconds are converted to frames, based on the Timeline settings. For example, if the timeline is expressed as seconds with a frame rate of 30 frames per second, entering 180 in the Playhead Location field converts 180 frames to seconds and moves the Timeline Playhead to 6:00.

To set the time format used by the Timeline Editor window, use the [Timeline Settings](TimelineSettings).

---
* <span class="page-edit">2017-08-10  <!-- include IncludeTextNewPageSomeEdit --></span>
