#Cursor locking and full-screen mode in WebGL

Cursor locking (using __[Cursor.lockState](ScriptRef:Cursor-lockState.html)__) and full-screen mode (using __[Screen.fullScreen](ScriptRef:Screen-fullScreen.html)__) are both supported in Unity WebGL, implemented using the respective HTML5 APIs (Element.requestPointerLock and Element.requestFullscreen). These are supported in Firefox and Chrome. Safari cannot currently use full-screen and cursor locking.

##Enabling cursor locking and full-screen mode in WebGL

Due to security concerns, browsers will only allow locking the cursor or going into full-screen mode in direct response to a user-initiated event (like a mouse click or key press). Unfortunately, Unity does not have separate event and rendering loops, so it defers event handling to a point where the browser no longer acknowledges a full-screen or cursor lock request issued from Unity scripting as a direct response to the event which triggered it. As a result, Unity triggers the request on the next user-initiated event, rather than the event that triggered the cursor lock or full-scree request.

To make this work with acceptable results, you should trigger cursor locking or full-screen requests on mouse/key down events, instead of mouse/key up events. This ensures that when the request is deferred to the next user-initiated event, it is triggered when the user releases the mouse or key.

If you use Unity's [UI.Button](ScriptRef:UI.Button.html) component, you can achieve the desired behaviour by creating a subclass of `Button`, which overrides the [OnPointerDown](ScriptRef:UI.Selectable.OnPointerDown.html)
 method.
 
Note that browsers may show a notification message or ask the user for permission before entering full-screen mode or locking the cursor.