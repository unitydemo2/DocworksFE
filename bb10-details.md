#Blackberry10 Details


##Player Settings

The BlackBerry tab in the Player Settings (menu: __Edit &gt; Project Settings &gt; Player__) provides settings which can be configured for your application.

![Blackberry10 Other Settings](../uploads/Main/bb10othersettings.png) 

_Microphone_ is NOT enabled on BlackBerry (retained in the UI as it is a common feature among mobile devices).


##Touch

On Blackberry10 [Touch](ScriptRef:Input.GetTouch.html) events are handled just like other mobile platforms. Note however that the touch area on the Z10 is larger than the screen area. This means the returned finger position can be off the edge of the screen, with values negative, and/or greater than the screen width and/or height. 
