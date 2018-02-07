#Input in WebGL

##Gamepad and Joystick support

Gamepads and Joysticks are supported in WebGL (using the __[Input](ScriptRef:Input.html)__ class) on browsers which support the HTML5 Gamepad API. Check our [browser compatibilty table](webgl-browsercompatibility) to see which browsers these are.

Note that browsers may only allow access to available input devices once the user has interacted with the device while the content has focus. This is a security measure to prevent using the connected devices for browser fingerprinting purposes. For this reason, you should make sure to instruct the user to click a button on their devices before checking __[Input.GetJoystickNames()](ScriptRef:Input.GetJoystickNames.html)__) for connected devices.

##Touch support

While Unity WebGL [does not officially](webgl-browsercompatibility) support mobile devices yet, __[Input.touches](ScriptRef:Input-touches.html)__ and related APIs are implemented on browsers and devices with touch support - as well as __[Input.acceleration](ScriptRef:Input-acceleration.html)__.

##Keyboard input and focus handling

By default, Unity WebGL will process all keyboard input send to the page, regardless of whether the WebGL canvas has focus or not. This is done so that a user can start playing a keyboard-based game right away without the need to click on the canvas to focus it first. However, this can cause problems when there are other HTML elements on the page which should receive keyboard input, such as text fields - as Unity will consume the input events before the rest of the page can get them. If you need to have other HTML elements receive keyboard input, you can change this behavior using the __WebGLInput.captureAllKeyboardInput__ property.
