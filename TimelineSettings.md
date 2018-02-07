## Timeline Settings

Use the Timeline Settings to set the unit of measurement for the Timeline Asset, to set the duration mode of the Timeline Asset, and to set the Timeline Editor window snap settings.

![Click the Cog icon in the Timeline Editor window to view the Timeline Settings menu](../uploads/Main/timeline_cog_menu.png)

### Seconds or Frames

Select either Seconds or Frames to set the Timeline Editor window to display time in either seconds or frames.

### Duration Mode

Use the Duration Mode to set whether the duration of the Timeline Asset extends to the end of the last clip (Based On Clips), or extends to a specific time or frame (Fixed Length). When the Duration Mode is set to Fixed Length, use one of the following methods to change the length of the Timeline Asset:

* Select the Timeline Asset in the Project window and use the Inspector window to set the Duration in seconds or frames. 

* In the Timeline Editor window, drag the blue marker on the timeline. The blue marker indicates the end of the Timeline Asset. A blue line indicates the duration of the Timeline Asset.

![Timeline Asset duration (red rectangle) and end marker (green circle)](../uploads/Main/timeline_duration_mode.png)

### Frame Rate

Select one of the options under frame rate to set the play speed of the Timeline Asset. The overall speed of the Timeline Asset accelerates or decelerates based on the number of frames per second. The higher the number of frames per second, the faster the entire timeline plays. The following frame rates are supported: Film (24 fps), PAL (25 fps), NTSC (29.97 fps), 30, 50, or 60.  

### Show Audio Waveforms

Enable __Show Audio Waveforms__ to draw the waveforms for all audio clips on all audio tracks. For example, use an audio waveform as a guide when manually positioning an Audio clip of footsteps with the Animation clip of a humanoid walking. Disable __Show Audio Waveform__ to hide audio waveforms. __Show Audio Waveforms__ is enabled by default.


### Snap to Frame

Enable __Snap to Frame__ to manipulate clips, preview Timeline instances, drag the playhead, and position the playhead using frames. Disable __Snap to Frame__ to use subframes. __Snap to Frame__ is enabled by default.

For example, when __Snap to Frame__ is disabled and you drag the Timeline Playhead, it moves the playhead between frames, the format of Playhead Location displays differently depending on whether the timeline is set to __Seconds__ or __Frames__:

* When the timeline is set to __Frames__, the Playhead Location field shows frames and subframes. For example, 8 frames and 34 subframes displays as 8.34.

* When the timeline is set to __Seconds__, the Playhead Location field shows seconds, frames, and subframes. For example, 6 seconds, 17 frames, and 59 subframes displays as 6:17 [.59].

![Disable Snap to Frame to position clips and drag the playhead between frames](../uploads/Main/timeline_frames_subframes.png)

Manipulating clips, previewing Timeline instances, and positioning the playhead at the subframes level is useful when attempting to synchronize animation and effects with audio. Many high-end audio processing software products create audio waveforms with subframe accuracy. 

### Edge Snap

Enable the __Edge Snap__ option to snap clips during positioning, trimming, and creating blends. When enabled, clips are snapped when the start or end of a clip is dragged within 10 pixels of the start or end of a clip on another track, the start or end of a clip on the same track, the start or end of the entire timeline, or the playhead. Disable __Edge Snap__ to create accurate blends, ease-ins, or ease-outs. __Edge Snap__ is enabled by default.

---
* <span class="page-edit">2017-12-07  <!-- include IncludeTextAmendPageSomeEdit --></span>
