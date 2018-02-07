### Reordering tracks and rendering priority

The rendering and animation priority of tracks is from top to bottom. Reorder tracks to change their rendering or animation priority.

For example, if a Track list contains two Animation tracks that animate the position of a GameObject, the second track overrides the animation on the first track. The animation priority is the reason why Animation Override tracks are added as child tracks under Animation tracks.

To reorder tracks, select one or more tracks and drag until a white insert line appears between tracks in the Track list. The white insert line indicates the destination of the tracks being dragged. Release the mouse button to reorder tracks.

An Animation Override track is bound to the same GameObject as its parent Animation track. Reordering an Animation Override track converts it to an Animation track and resets its binding to none.


---
* <span class="page-edit">2017-12-07  <!-- include IncludeTextAmendPageSomeEdit --></span>
