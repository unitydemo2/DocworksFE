# Advanced Unity mobile scripting

## Device properties

There are a number of device-specific properties that you can access when developing for mobile. See the Unity Scripting API pages for [SystemInfo.deviceUniqueIdentifier](ScriptRef:SystemInfo-deviceUniqueIdentifier.html), [SystemInfo.deviceName](ScriptRef:SystemInfo-deviceName.html),[SystemInfo.deviceModel](ScriptRef:SystemInfo-deviceModel.html), and [SystemInfo.operatingSystem](ScriptRef:SystemInfo-operatingSystem.html) for more information.

## Anti-piracy check

Pirates often hack an app by removing DRM protection and then redistributing it for free. Unity comes with an anti-piracy check, which is used to determine if your app was altered after it was submitted to the Google Play Store.

To check if your app is genuine (meaning it is not hacked), use the Unity Scripting API [Application.genuine](ScriptRef:Application-genuine.html) property. If this property returns `false`, you can inform the app user that they are using a hacked app or you can disable access to some functions of your app.

**Note:** Use [Application.genuineCheckAvailable](ScriptRef:Application-genuineCheckAvailable.html) along with [Application.genuine](ScriptRef:Application-genuine.html) to verify app integrity. Accessing the [Application.genuine](ScriptRef:Application-genuine.html) property is a resource-intensive operation, so do not call it during frame updates or other time-critical code.

## Vibration support

To trigger a vibration, call [Handheld.Vibrate](ScriptRef:Handheld.Vibrate.html) in your code. Devices lacking vibration hardware ignore this call.

## Activity indicator

Mobile operating systems have built-in activity indicators that you can activate during slow operations. 

Refer to the [Activity Indicator Unity Scripting API](ScriptRef:Handheld.StartActivityIndicator.html) documentation for examples.

## Screen orientation

When creating Projects for iOS and Android, you can control the screen orientation of a user's device. Detecting a change in orientation or forcing a specific orientation is useful for altering game behavior depending on how the user is holding their device.

To retrieve device orientation, use the [Screen.orientation](ScriptRef:Screen-orientation.html) property. Orientation can be one of the following:

| **Orientation** | **Behavior**  |
|:---|:---| 
| Portrait| The device is in portrait mode, with the device held upright and the home button at the bottom. |
| PortraitUpsideDown| The device is in portrait mode but upside-down, with the device held upright and the home button at the top. |
| LandscapeLeft| The device is in landscape mode, with the device held upright and the home button on the right side. |
| LandscapeRight| The device is in landscape mode, with the device held upright and the home button on the left side. |

Control screen orientation  by setting [Screen.orientation](ScriptRef:Screen-orientation.html) to one of the above options, or to [ScreenOrientation.AutoRotation](ScriptRef:ScreenOrientation.AutoRotation.html).

When using auto-rotation, you can disable some orientations on a case-by-case basis. See the Scripting API pages for [Screen.autorotateToPortrait](ScriptRef:Screen-autorotateToPortrait.html), [Screen.autorotateToPortraitUpsideDown](ScriptRef:Screen-autorotateToPortraitUpsideDown.html), [Screen.autorotateToLandscapeLeft](ScriptRef:Screen-autorotateToLandscapeLeft.html), and [Screen.autorotateToLandscapeRight](ScriptRef:Screen-autorotateToLandscapeRight.html) for more information.

----
* <span class="page-edit">2017-05-25 <!-- include IncludeTextNewPageYesEdit --></span>

* <span class="page-history">Updated functionality in 5.5</span>