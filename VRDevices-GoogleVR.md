# Google VR

Google VR encompasses both Daydream and Cardboard, two VR platforms owned by Google. See [Google’s VR documentation](https://developers.google.com/vr/) for more information about the requirements and functionality of each.

Google VR applications are developed using Daydream. Daydream for Unity is a technical preview designed to give Unity developers early access to Google VR development. See [Google’s Daydream documentation](https://developers.google.com/vr/unity/) for more information about this.

This page provides a step-by-step guide to configuring Unity for Daydream development, and provides information on what you need to be aware of while developing for Daydream. 

## Getting started

Daydream’s minimum system requirement is Android API SDK version 21 (also known as "Lollipop"). If you don’t already have Lollipop, download it from the [Google Android developer site](http://developers.android.com). 

You also need a Daydream-enabled phone. See [Google’s documentation on Daydream hardware](https://developers.google.com/vr/concepts/dev-kit-setup) to learn how to set your Android phone up for Daydream development.

## Configuring Unity for Daydream development

1. In the main menu, go to __Edit__ > __Project Settings__ > __Player__.

2. Click the Android logo to apply settings for building to Android (Box 1 in figure below).

3. Open __Other Settings,__ and under the __Rendering__ section, tick the __Virtual Reality Supported__ checkbox.

![](../uploads/Main/VRDevices-GoogleVR1.png)

A list called Virtual Reality SDKs appears. Select the plus (__+__) icon at the bottom of the list.

![](../uploads/Main/VRDevices-GoogleVR2.png)

From the drop-down, select __Daydream__. This then appears in the __Virtual Reality SDKs__ list. Select the drop-down arrow next to it to expand the Daydream settings.

![](../uploads/Main/VRDevices-GoogleVR3.png)

| __Property__| __Function__ |
|:---|:---| 
| __Depth Format__| Use this drop-down to set the Z buffer depth. This is used for sorting the visible data and determining what is actually rendered to the screen. |
| __Foreground Icon__| Set the foreground icon for presentation in the VR Google Play store. |
| __Background Icon__| Set the background icon for presentation in the VR Google Play store. |
| __Use Sustained Performance Mode__| Enable Sustained Performance Mode for longer VR experiences. This reduces performance to improve battery life. |

The minimum platform requirement for Daydream is Android 7.0 Lollipop (API level 21). To ensure Unity uses the correct APK, and only runs on devices upgraded to the latest version of Android, you need to change the __Minimum API Level__. 

To do this in the Player Settings, navigate to __Other Settings__ and under __Identification__ use the __Minimum API Level__ drop-down to set it to the latest API in the list. 

![](../uploads/Main/VRDevices-GoogleVR4.png)

__Target API Level__ should be set to API level 21 or higher for Cardboard and Daydream. By default, this property uses the highest level you have installed. For more information about API levels for Android, see documentation on [Android PlayerSettings](class-PlayerSettingsAndroid).

You are now ready create your Unity content for Daydream. Follow the same workflow you would for normal Android development (see documentation on [Android development](android) for more information), and ensure when you build and run your game (menu: __File__ > __Build & Run__), you build and run it on a Daydream-capable phone. 

## Working with Daydream for Unity

When working with Daydream for Unity, note the following:

* Use the device names `daydream` and `cardboard` to load a specific device when you want to enable VR for that device. To do this, call [VRSettings.LoadDeviceByName](ScriptRef:VR.VRSettings.LoadDeviceByName.html) and pass in the string name of the device.

* Rendering is done side-by-side, over a single, double-wide Texture.

* Integration of Daydream for Unity takes over the Unity activity’s view hierarchy. This means that any modification you make to the view hierarchy before you initialize Daydream for Unity is removed while in VR mode.

### Daydream and Google Cardboard

__Daydream__ and __Cardboard__ have separate entries in the __Virtual Reality SDKs__ list. Unity reads the list from top to bottom until it finds a device configuration that works, so the addition, removal or ordering of these devices in that list have consequences on built application functionality.

* If __Cardboard__ is above __Daydream__ in the __Virtual Reality SDKs__ list, the application might not run in Daydream mode, even on Daydream hardware.

* If __Daydream__ is the only item in the __Virtual Reality SDKs__ list, VR Android Manifest entries are added so that the app appears in the VR-specific Google Play store. Asynchronous reprojection is a requirement for Daydream, so all devices which support Daydream also support asynchronous reprojection.

* If __Cardboard__ is the only item in the __Virtual Reality SDKs__ list, the app does not appear in the VR Google Play store. Asynchronous reprojection and sustained performance mode are not enabled, even on capable hardware.

* If both __Daydream__ and __Cardboard__ are in the __Virtual Reality SDKs__ list, Asynchronous reprojection is enabled if running on supported hardware. Sustained performance mode is enabled if selected and if running on supported hardware. The app appears in all Google Play Stores.

### Other VR SDKs

* If you plan to support GearVR as well as Daydream and Cardboard, place __Oculus__ at the top of the list. Phones that support GearVR run through the GearVR SDK, and phones that don’t support it fall back to Daydream or Cardboard.

* If you add __None__ as the first device in the list, Unity starts as a normal application and can be toggled into VR through script. See API documentation on [VRSettings.enabled](ScriptRef:VR.VRSettings-enabled.html) and [VRSettings.LoadDeviceByName](ScriptRef:VR.VRSettings.LoadDeviceByName.html) for more information.

### Magic Window mode

Sometimes, you might want to apply a non-stereoscopic view with head tracking applied (for example, if you want to view a 2D image in VR, or provide a 2D preview of your VR application). This can be useful for promotional materials. To facilitate this, you can access head tracking data when [VRSettings.enabled](ScriptRef:VR.VRSettings-enabled.html) equals false and the [VRSettings.loadedDeviceName](ScriptRef:VR.VRSettings-loadedDeviceName.html) is `daydream` or `cardboard`. 

For example:

```

UnityEngine.VR.VRSettings.enabled = false;
Camera.main.GetComponent<Transform>().localRotation = UnityEngine.VR.InputTracking.GetLocalRotation(VRNode.CenterEye);

```

See API documentation on [VRSettings.LoadDeviceByName](ScriptRef:VR.VRSettings.LoadDeviceByName.html) for more information. 

### Hardware volume controls

Daydream for Unity blocks the native OS from handling the hardware volume controls. This stops the OS from bringing up the volume UI when in VR mode. To handle the hardware volume controls yourself, extend the standard `UnityPlayerActivity` and handle `onKeyDown` and `onKeyLongPress` yourself. 

For more information about this please see documentation on [plug-ins for Android](PluginsForAndroid). 

Unity does not block the volume controls from the Daydream controller.

### Overriding Android libraries provided by Daydream

Daydream for Unity integration ships with two libraries to support Daydream development:

* Daydream native library: _gvr.aar_

* Google Protobuf Nano Java library: _libprotobuf-java-nano.jar_

You can override either of these libraries with newer or different versions of the libraries with the same name located in the _Assets/Plugins/Android_ project folder. Names must match exactly in order for them to be correctly overridden.

### API support

The following APIs are not supported by Daydream for Unity:

* `VRSettings.showDeviceView`

* `VRDevice.isPresent`

* `VRDevice.refreshRate`

* `VRStats.gpuTimeLastFrame`

