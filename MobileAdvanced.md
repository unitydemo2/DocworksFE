
Device Properties
-----------------

There are a number of device-specific properties that you can access. See the script reference pages for [SystemInfo.deviceUniqueIdentifier](ScriptRef:SystemInfo-deviceUniqueIdentifier.html), [SystemInfo.deviceName](ScriptRef:SystemInfo-deviceName.html), [SystemInfo.deviceModel](ScriptRef:SystemInfo-deviceModel.html) and [SystemInfo.operatingSystem](ScriptRef:SystemInfo-operatingSystem.html).


Anti-Piracy Check
-----------------

Pirates will often hack an application (by removing AppStore DRM protection) and then redistribute it for free. Unity comes with an anti-piracy check which allows you to determine if your application was altered **after** it was submitted to the AppStore.

You can check if your application is genuine (not-hacked) with the [Application.genuine](ScriptRef:Application-genuine.html) property. If this property returns __false__ then you might notify user that they are using a hacked application or maybe disable access to some functions of your application.

**Note:** [Application.genuineCheckAvailable](ScriptRef:Application-genuineCheckAvailable.html) should be used along with __Application.genuine__ to verify that application integrity can actually be confirmed. Accessing the [Application.genuine](ScriptRef:Application-genuine.html) property is a fairly expensive operation and so you shouldn't do it during frame updates or other time-critical code.

Vibration Support
-----------------

You can trigger a vibration by calling [Handheld.Vibrate](ScriptRef:Handheld.Vibrate.html). However, devices lacking vibration hardware will just ignore this call.

Activity Indicator
------------------

Mobile OSs have built-in activity indicators, that you can use during slow operations. Please check [Handheld.StartActivityIndicator docs](ScriptRef:Handheld.StartActivityIndicator.html) for usage sample.

Screen Orientation
------------------

Unity iOS/Android/Tizen allows you to control current screen orientation. Detecting a change in orientation or forcing some specific orientation can be useful if you want to create game behaviors depending on how the user is holding the device.

You can retrieve device orientation by accessing the [Screen.orientation](ScriptRef:Screen-orientation.html) property. Orientation can be one of the following:

| | |
|:---|:---|
|__Portrait__ |The device is in portrait mode, with the device held upright and the home button at the bottom.|
|__PortraitUpsideDown__ |The device is in portrait mode but upside down, with the device held upright and the home button at the top.|
|__LandscapeLeft__ |The device is in landscape mode, with the device held upright and the home button on the right side.|
|__LandscapeRight__ |The device is in landscape mode, with the device held upright and the home button on the left side.|

You can control screen orientation by setting [Screen.orientation](ScriptRef:Screen-orientation.html) to one of those, or to [ScreenOrientation.AutoRotation](ScriptRef:ScreenOrientation.AutoRotation.html).
When you want auto-rotation, you can disable some orientation on a case by case basis. See the script reference pages for [Screen.autorotateToPortrait](ScriptRef:Screen-autorotateToPortrait.html), [Screen.autorotateToPortraitUpsideDown](ScriptRef:Screen-autorotateToPortraitUpsideDown.html), [Screen.autorotateToLandscapeLeft](ScriptRef:Screen-autorotateToLandscapeLeft.html) and[Screen.autorotateToLandscapeRight](ScriptRef:Screen-autorotateToLandscapeRight.html)

