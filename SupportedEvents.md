Supported Events
=================
The Event System supports a number of events, and they can be customised further in user custom user written Input Modules.

The events that are supported by the Standalone Input Module and Touch Input Module are provided by interface and can be implemented on a MonoBehaviour by implementing the interface. If you have a valid Event System configured the events will be called at the correct time.

- IPointerEnterHandler - OnPointerEnter - Called when a pointer enters the object
- IPointerExitHandler - OnPointerExit - Called when a pointer exits the object
- IPointerDownHandler - OnPointerDown - Called when a pointer is pressed on the object
- IPointerUpHandler - OnPointerUp - Called when a pointer is released (called on the GameObject that the pointer is clicking)
- IPointerClickHandler - OnPointerClick - Called when a pointer is pressed and released on the same object
- IInitializePotentialDragHandler - OnInitializePotentialDrag - Called when a drag target is found, can be used to initialise values
- IBeginDragHandler - OnBeginDrag - Called on the drag object when dragging is about to begin
- IDragHandler - OnDrag - Called on the drag object when a drag is happening
- IEndDragHandler - OnEndDrag - Called on the drag object when a drag finishes
- IDropHandler - OnDrop - Called on the object where a drag finishes
- IScrollHandler - OnScroll - Called when a mouse wheel scrolls
- IUpdateSelectedHandler - OnUpdateSelected - Called on the selected object each tick
- ISelectHandler - OnSelect - Called when the object becomes the selected object
- IDeselectHandler - OnDeselect - Called on the selected object becomes deselected
- IMoveHandler - OnMove - Called when a move event occurs (left, right, up, down, ect)
- ISubmitHandler - OnSubmit - Called when the submit button is pressed
- ICancelHandler - OnCancel - Called when the cancel button is pressed