# Google VR SDK Overview

![](../uploads/Main/Logo_cardboard_small.png)
![](../uploads/Main/Logo_daydream.png)

[Virtual Reality Input](vr-input)Google VR is the technology behind both [Google Daydream](https://developers.google.com/vr/daydream/overview) and [Google Cardboard](https://developers.google.com/vr/cardboard/overview) VR platforms. Google VR encompasses support for smartphones, head mounted viewers and controllers, standalone head mounted displays and applications. Google VR provides an SDK for Unity that allows you to build VR content for this rich ecosystem of devices.

Google VR technologies includes Daydream, a platform for high quality mobile VR and Cardboard, built for bite-size VR experiences and 360 video. Daydream consists of Daydream-ready phones, headsets, controllers and experiences and supports high-end Android mobile devices through [Daydream](https://vr.google.com/daydream/smartphonevr/phones/). See the full list of Daydream devices on the [Google VR](https://vr.google.com/daydream/smartphonevr/phones/)) website. [Cardboard](https://vr.google.com/cardboard/developers/) works with almost any smartphone on both iOS and Android.

Google Cardboard is the most accessible mobile VR solution, allowing anyone with an iOS or Android smartphone to experience VR apps. Cardboard does have minimum and recommended requirements for its usage, but these are much less hardware-bound than Daydream, focusing mainly on the operating system and basic control systems (such as the [gyroscope](https://en.wikipedia.org/wiki/Gyroscope)). Users can view VR apps with an official Google Cardboard viewing device, or a third-party VR viewing device which supports Google VR content (See Hardware and Software Requirements section). Cardboard also supports a range of third-party handheld controllers, for apps which require more complex interactions.

Daydream allows more feature-rich experiences than Cardboard, but only supports Daydream ready devices such as  Daydream-ready phones, built for VR with high-resolution displays, smooth graphics and high fidelity sensors for precise head tracking. Daydream phone apps are accessible with the Daydream View, Google’s headset and motion controller for experiencing high quality VR, using a Daydream-ready phone. Daydream will also support a Daydream Standalone HMD built by original design manufacturers. Daydream Standalone is an untethered head mounted display running on the Android OS including richer controller input and motion tracking.

See [Google’s VR documentation](https://developers.google.com/vr/) for more information about the requirements and functionality of Cardboard and Daydream.

## __Hardware and software requirements__

This section provides an overview of both the minimum and recommended hardware and software requirements for using the Google VR SDK.

Below are the minimum platform requirements for devices to support the Google VR SDK, along with some important considerations:

* You must have Android API SDK version 21 (also known as "Lollipop") installed. 

* To develop Google VR applications, you must have a Cardboard- or Daydream-supported phone. 

* See Google’s documentation on [Daydream hardware](https://developers.google.com/vr/concepts/dev-kit-setup) to learn how to set your Android phone up for Daydream development.

### __Minimum hardware and software requirements__

This section provides an overview of the minimum hardware and software requirements for developing with the Google VR SDK.

| Device| Hardware | Software |
|:---|:---|:---| 
| Cardboard| - Devices running Android 4.1 or later with a gyroscope.<br/>- Devices running iOS 8 or later with a gyroscope.<br/>- A viewing device compatible with Cardboard. | - Unity Cardboard integration requires Android Lollipop or greater.<br/>- iOS devices with the Google Cardboard application installed.
| Daydream| - Daydream compatible devices. See the [Google Daydream Hardware](https://developers.google.com/vr/daydream/hardware) page for a list of devices compatible with Daydream. |  |

### __Recommended hardware and software requirements__

This section provides an overview of the recommended hardware and software requirements for developing with the Google VR SDK.

| Device| Hardware | Software |
|:---|:---|:---| 
| Cardboard| - For Android, refer to the documentation provided with your Cardboard viewer for a full list of compatible devices.<br/>- For iOS, any iPhone 5 series or later phone.<br/>- A viewing device compatible with Cardboard. | - Android 5.0 or later.<br/>- iOS 8 or later, with the Google Cardboard application installed. |
| Daydream| - Any device compatible with the Daydream specification. See the [Google Daydream Hardware](https://developers.google.com/vr/daydream/hardware) page for a list of devices compatible with Daydream. | Android 7 or later. |

You can find detailed information relating to Google VR development on the main [Google developer site for VR](https://developers.google.com/vr/). This site includes links to SDKs, instructional materials, and documentation on APIs and store publishing.

## __Quick start guide__

This section helps you get started with developing Google VR applications using Unity. Many of the instructions for developing Google VR content are available on the [Google VR Developer website](https://developers.google.com/vr/).

To install Unity and use the external links for platform-specific setup instructions for the Google VR SDK:

1. Use the [Installing Unity manual guide](InstallingUnity) to help install the Unity Editor.

    i ) When targeting Android make sure to install Unity Android Support through the __Unity installer__.

    ii ) When targeting iOS, make sure you install Unity iOS support through the      __Unity Installer__ and that you have a macOS machine to compile and deploy to your device.

2. Follow the instructions laid out on the [Google developer site for VR](https://developers.google.com/vr/) for your targeted platform(s).

Google provides starter guides for developing Google VR applications with Unity for both Android and iOS. Links to specific guides are given below:

* Getting started with [Google VR SDK for Unity for Android](https://developers.google.com/vr/unity/get-started).

* Getting started with [Google VR SDK for Unity for iOS](https://developers.google.com/vr/unity/get-started-ios).

## __Platform configuration settings__

This section provides a step-by-step guide for configuring your Unity Project to build Google VR applications.

Follow the steps in the next sections to ensure your Unity project can successfully build for your target Google VR devices.

### __Targeting Cardboard (Android and iOS)__

Unity provides a number of platform-specific build options for building applications to Cardboard-supported devices. 

To access these settings, open the __Player Settings__ (menu: __Edit__ > __Project Settings__ > __Player__) and navigate to either the Android or iOS section (click either on the iPhone or Android icon) depending on which device you want to build to. Navigate to __XR Settings__ and make sure the __Virtual Reality Supported__ checkbox is ticked. Next, navigate to the __Virtual Reality SDKs__ list and click the plus __(+)__ button. Select __Cardboard__ to add it to the list.

![Finding Cardboard-specific settings for iOS/Android (Edit > Project Settings > Player > XR Settings)](../uploads/Main/cardboard_settings.png)

When you have added __Cardboard__ to the __Virtual Reality SDKs__ list, click the foldout arrow next to it to view additional __Cardboard__ settings.

![Cardboard-specific settings in VR SDK list](../uploads/Main/additional_cardboard_settings.png)


The table below provides a list of properties available in the __Cardboard__ settings, along with a description of their functionality.

| __Property__| __Description<br/>__  |
|:---|:---| 
| __Depth Format__| Use this drop-down to set the Z buffer depth. Unity uses this to sort the visible data and determine what is actually rendered to the  screen. |
| __Enable Transition View__| The transition view is the view that Google VR provides to inform the user that they must put their device in a Cardboard compatible viewer. You can enable it to provide users some time to insert their device into a viewer. By default this is disabled but it can be enabled to provide some time for the user to insert their device into a viewer. |


The minimum platform requirement for Cardboard is Android 5.0 (Lollipop) (SDK API level 21). 

To ensure Unity uses the correct APK, and only runs on devices upgraded to the latest version of Android, you need to change the __Minimum API Level__.

To do this, go to Player Settings and navigate to __Other Settings__. Under __Identification,__ use the __Minimum API Level__ drop-down to set it to the latest API in the list.

Set the __Target API Level__ to API level 21 or higher for Cardboard only. If you are targeting Daydream then this needs to be 24 or higher. By default, this property uses the highest level you have installed. For more information about API levels for Android, see documentation on [Android PlayerSettings](class-PlayerSettingsAndroid).

You are now ready to create your Unity content for Cardboard. Follow the same workflow you would for normal Android or iOS development (see documentation on [Android development](android) or [iOS development](iphone) for more information). Make sure you build and run your game on a Cardboard-capable device (menu: __File__ > __Build & Run__).

### __Targeting Daydream (Android only)__

Unity provides a number of platform-specific build options for building applications to Daydream-supported devices. 

To access these settings, open the __Player Settings__ (menu: __Edit__ > __Project Settings__ > __Player__) and navigate to the Android section (click the Android icon marked in the figure below). Navigate to __XR Settings__ and make sure the __Virtual Reality Supported__ checkbox is ticked. Next, navigate to the __Virtual Reality SDKs__ list and click the plus (+) button. Select __Daydream__ to add it to the list.

![Finding the Daydream-specific settings for Android (Edit > Project Settings > Player > XR Settings)](../uploads/Main/Daydream_settings.png)


When you add __Daydream__ to the __Virtual Reality SDKs__ List, click the foldout arrow next to it to view additional Daydream settings.

![Daydream-specific settings in VR SDK list](../uploads/Main/Daydream_VR_list.png)


The table below provides a list of properties available in the Daydream settings, along with a description of their functionality.

| __Property__| __Description<br/>__ |
|:---|:---| 
| __Depth Format__| Use this drop-down to set the Z buffer depth. This is used for sorting the visible data and determining what is actually rendered to the screen. |
| __Foreground Icon__| Set the foreground icon for presentation in the Google VR Play store. |
| __Background Icon__| Set the background icon for presentation in the Google VR Play store. |
| __Use Sustained Performance Mode__| Enable __Sustained Performance Mode__ for longer XR experiences. This reduces performance to improve battery life. |
| __Enable Video Surface__| Enable Asynchronous Video Reprojection. For more information,  see the documentation about [Asynchronous Video Reprojection](VRDevices-GoogleVRVideoAsyncReprojection) for more information. |
| __Enable Protected Memory__| Enables memory protection for DRM protected content when using Asynchronous Video Reprojection. This option only appears if __Enable Video Surface__ has been selected. For more information, see [Asynchronous Video Reprojection](VRDevices-GoogleVRVideoAsyncReprojection) |

Properties available for Daydream in Unity Player Settings

The minimum platform requirement for targeting Daydream only is Android 7.0 (Nougat) (SDK API level 24). If you are targeting Cardboard as well as Daydream, then the minimum supported API level is 21.

To ensure Unity uses the correct APK, and only runs on devices upgraded to the latest version of Android, you need to change the __Minimum API Level__.

To do this in the Player Settings, navigate to __Other Settings__. Under __Identification,__ use the __Minimum API Level__ drop-down to set it to the latest API in the list. 

Set __Target API Level__ should be set to API level 24 if you are Daydream. By default, this property uses the highest level you have installed. For more information about API levels for Android, see documentation on [Android PlayerSettings](class-PlayerSettingsAndroid).

You are now ready to create your Unity content for Daydream. Follow the same workflow you would for normal Android development (see documentation on [Android development](android) for more information). Make sure you build and run your game on a Daydream-capable device (menu: __File__ > __Build & Run__).

## __Working with Google VR for Unity__

This section covers important considerations you should keep in mind when creating Google VR content in Unity. 

When working with Google VR for Unity, note the following:

* Use the device names daydream and cardboard to load a specific device when you want to enable XR for that device. To do this, call [XRSettings.LoadDeviceByName](ScriptRef:XR.XRSettings.LoadDeviceByName.html) and pass in the string name of the device.

* Integration of Daydream for Unity takes over the Unity activity’s view hierarchy. This means that any modification made to the view hierarchy before initializing Daydream for Unity, is removed while in XR mode.

### __Daydream and Cardboard__

__Daydream__ and __Cardboard__ have separate entries in the __Virtual Reality SDKs__ list (__File__ > __Project Settings__ > __Player__ > __XR Settings__). Unity reads the list from top to bottom until it finds a device configuration that works. 

Removing or reordering the SDKs in the list affects the functionality of your final built application, as detailed below:

* If both __Daydream__ and __Cardboard__ are in the __Virtual Reality SDKs__ list, asynchronous reprojection is enabled if running on hardware that supports it. __Sustained Performance Mode__ is enabled if running on hardware that supports it, and if you have enabled it in the __Player Settings__ (see previous section on targeting Daydream). The app appears in all Google Play Stores.

* If __Cardboard__ is above __Daydream__ in the __Virtual Reality SDKs__ list, the application might not run in Daydream mode, even on Daydream hardware.

* If __Daydream__ is the only item in the __Virtual Reality SDKs__ list, Unity adds XR Android manifest entries so that the app appears in the XR-specific Google Play store. Daydream requires asynchronous reprojection, so all devices which support Daydream also support asynchronous reprojection.

* If __Cardboard__ is the only item in the __Virtual Reality SDKs__ list, the app does not appear in the Google VR Play store. Asynchronous reprojection and __Sustained Performance Mode__ are disabled, even on capable hardware.

* If you plan to support GearVR as well as Daydream and Cardboard, place __Oculus__ at the top of the list. Phones that support GearVR run through the GearVR SDK, and phones that don’t support it fall back to __Daydream__ or __Cardboard__.

* If you add __None__ as the first device in the list, Unity starts as a normal application and you can toggle XR through script. See API documentation on [XRSettings.enabled](ScriptRef:XR.XRSettings-enabled.html) and [XRSettings.LoadDeviceByName](ScriptRef:XR.XRSettings.LoadDeviceByName.html) for more information.

### __Cardboard for iOS__

Google distributes the __Cardboard Native Development Kit__ (NDK) for iOS through the [Cocoapods library management system](https://cocoapods.org). The Unity integration of Google VR uses a specific version of the __Cardboard NDK__ from the Cocoapods manager and this NDK is also used to create your XCode project.

This means the resulting project is generated differently from a standard Unity project. Cocoapods creates a wrapping __XCode__ workspace containing the Unity project as well as a project for the __Cardboard__ __NDK__ library and its dependencies. Always make sure that you open and/or use the workspace and not just the project to avoid linker errors due to the missing libraries in Cocoapods.

### __Magic Window mode__

During development, you may want to have a __non-stereoscopic view__ which still utilizes headtracking. This is useful if you require the user to view a 2D image in __XR__, or to provide 2D previews of your __XR application__. This can also be useful for promotional materials. To achieve this, you can access __head tracking data__ when the [__XRSettings.enabled__](ScriptRef:XR.XRSettings-enabled.html) property is false and the [__XRSettings.loadedDeviceName__](ScriptRef:XR.XRSettings-loadedDeviceName.html) is set to __daydream__ or __cardboard__.

The following example C# code rotates the main camera in a scene by using XR head tracking while disabling stereoscopic view using __XRSettings__:

```
UnityEngine.XR.XRSettings.enabled = false;
Camera.main.GetComponent<Transform>().localRotation = UnityEngine.XR.InputTracking.GetLocalRotation(XRNode.CenterEye);
```

For more information on the above, see the API documentation on [XRSettings.LoadDeviceByName](ScriptRef:XR.XRSettings.LoadDeviceByName.html).

### __Hardware volume controls__

The Daydream SDK for Unity prevents the native Operating System (OS) from accessing the device’s volume controls. This prevents the OS from displaying the volume user interface (UI) when in XR mode. To access the device’s volume controls manually, extend the standard __UnityPlayerActivity __(the primary Java class for the Unity Player on Android) and override the onKeyDown and onKeyLongPress key event functions yourself.

For more information on this process, see the Unity documentation on [extending the UnityPlayerActivity class](AndroidUnityPlayerActivity) through Java.

__Note:__ Unity does not block the volume controls on __Daydream__ controller, so if you only intend to use the controller in your game you may decide not to extend the __UnityPlayerActivity__ at all.

### __Overriding Daydream Android libraries__

The __Daydream SDK__ for Unity provides two libraries to support development for Daydream devices:

* Daydream native library: *gvr.aar*

* [Google Protobuf](https://developers.google.com/protocol-buffers/) Nano Java library: *libprotobuf-java-nano.jar*

You can replace either of these libraries by placing different versions of the library files in the **_Assets/Plugins/Android_** folder in your project. Library file names must match exactly in order for them to be correctly overridden.

### __Stereo Rendering methods__

Multi Pass rendering is supported on all Google VR platforms. [Single Pass rendering](Android-SinglePassStereoRendering) is supported only by Daydream on platforms that support driver level instancing.

## __Supported APIs and SDKs__

This section gives an overview of the supported APIs and SDKs for developing Google VR applications with Unity.

### __Unity API support__

The following APIs are __not__ __supported__ by Google VR for Unity:

* [XRSettings.showDeviceView](ScriptRef:XR.XRDevice.html)

* [XRDevice.isPresent](ScriptRef:XR.XRSettings.html)

* [XRStats.gpuTimeLastFrame](ScriptRef:XR.XRStats.html)

### __Supported graphics APIs__

The following __graphics__ __APIs__ are supported in Unity on both __Android__ and __iOS__ devices:

__Android__

* OpenGL

	

__iOS__

* Metal

* OpenGL

## Controllers and input devices

### __Daydream controller__

The Daydream controller allows 3 degrees of freedom, providing rotational and positional information, a dual axis touch/click controller along with 2 extra buttons. For information on how to take input from this device see the [Google Daydream Controller documentation](https://developers.google.com/vr/android/reference/com/google/vr/sdk/controller/package-summary).

![Daydream controller](../uploads/Main/Daydream_controller.png)

## __Features overview__

For full details on specific features provided by Google VR, see Google’s [Daydream Developer documentation](https://developers.google.com/vr/daydream/overview). For an overview of features supported by the Google VR SDK for Unity, see Google’s documentation on [Google VR for Unity](https://developers.google.com/vr/unity/).

The next section provides a short overview of Google VR supported features.

### __Supported feature sets__

The table below gives an overview of supported features for each target mobile VR device when working with Google VR in Unity.

|__Device__|__Platform__|__Rendering__|__Input__|
|:---|:---|:---|:---|
| Cardboard| Android Lollipop or later<br/> | - OpenGL<br/>- Stereo Instanced Rendering <br/>- Stereo Rendering | |
| Cardboard<br/>| iOS<br/> | - OpenGL<br/>- Metal<br/> -Stereo Instanced Rendering <br/> -Stereo Rendering| |
| Daydream| Android Nougat or later using compatible hardware | - OpenGL<br/>- Stereo Instanced Rendering <br/>- Stereo Rendering |Daydream controller |

## __Resources__

### Useful links

This section provides a number of useful external links for further reading into Google VR development topics.

* [VR section on Google developer website](https://developers.google.com/vr/)

* [Cocoapods](http://cocoapods.org)

### __Troubleshooting guide__

This section provides a list of the most common problems you may encounter when developing with the Google VR SDK.

| Problem| Suggestion |
|:---|:---| 
| I have a problem with GvrController/GvrViewer/GvrXXXX/Instant Preview. What do I do to resolve this?<br/>| These types are part of the Google VR SDK for Unity and are owned and supported by Google. While the general Unity community may be able to answer your questions, for any technical issues you should visit the [Google VR SDK for Unity](https://github.com/googlevr/gvr-unity-sdk) site on GitHUB.<br/> |
| When is the Daydream Keyboard going to be released?| The Daydream Keyboard for Google VR is a Google technology and will be released in some future version of the core Android system. Access and use of this technology is based solely on Google and the [Google VR SDK for Unity](https://github.com/googlevr/gvr-unity-sdk).<br/> |
| I am trying to build my Cardboard for iOS project, but Xcode is reporting linker errors.| Google distributes the Cardboard Native Development Kit (NDK) for iOS through the Cocoapods library management system. Unity is integrated with a specific version of that Cardboard NDK from the Cocoapods manager and uses the NDK to create your XCode project. The resulting project is generated differently from a standard Unity project. Cocoapods creates a wrapping XCode workspace containing the Unity project as well as a project for the Cardboard NDK library and its dependencies. Always make sure that you open and/or use the workspace and not just the project to avoid getting linker errors due to the missing libraries from Cocoapods. |



See the official Google VR developer website for more troubleshooting information for both [Cardboard](https://support.google.com/cardboard/answer/6295070?hl=en&ref_topic=6295055) and [Daydream](https://support.google.com/daydream/?hl=en-GB#topic=7184600).

---

* <span class="page-edit">2017-11-21 <!-- include IncludeTextNewPageYesEdit --></span>

* <span class="page-history">New functionality in 2017.2</span>
