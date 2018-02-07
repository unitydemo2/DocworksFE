# Vuforia SDK overview

![](../uploads/Main/vuforia_logo.png)

Vuforia is a cross-platform Augmented Reality (AR) and Mixed Reality (MR) application development platform, with robust tracking and performance on a variety of hardware (including mobile devices and mixed reality Head Mounted Displays (HMD) such as the Microsoft HoloLens). Unity’s integration of Vuforia allows you to create vision apps and games for Android and iOS using a drag-and-drop authoring workflow. A [Vuforia AR+VR samples package](https://www.assetstore.unity3d.com/en/#!/content/101547) is available on the Unity Asset Store, with several useful examples demonstrating the most important features of the platform.

Vuforia supports many third-party devices (such as AR/MR glasses), and VR devices with back-facing cameras (such as the Gear VR). See the Vuforia page on [Devices](https://www.vuforia.com/Devices) for a full list of supported devices. See the [Vuforia API reference](https://library.vuforia.com/content/vuforia-library/en/reference/unity/index.html) for more information about classes, properties and functions used in the SDK.

You can use any device with a camera to test AR/MR games and applications built in Unity with Vuforia.

## Important concepts

Before learning more about Vuforia and its supported features, you need to understand a number of important concepts. Among these concepts are forms of tracking and marker types commonly used in Vuforia applications.

### Marker-based tracking 

In AR or MR, markers are images or objects registered with the application which act as information triggers in your application. When your device’s camera recognizes these markers in the real world (while running an AR or MR application), this triggers the display of virtual content over the world position of the marker in the camera view. Marker-based tracking can use a variety of different marker types, including QR codes, physical reflective markers, Image Targets and 2D tags. The simplest and most common type of marker in game applications is an Image Target.

![Common Image Target types](../uploads/Main/target_types.png)


#### Image Targets

Image Targets are a specific type of marker used in Marker-based tracking. They are images you manually register with the application, and act as triggers that display virtual content. For Image Targets, use images containing distinct shapes with complex outlines. This makes it easier for image recognition and tracking algorithms to recognize them. 

### Markerless tracking

Applications using Markerless tracking are more commonly location-based or position-based Augmented or Mixed Reality. This form of tracking relies on technologies such as GPS, accelerometer, gyroscope and more complex image processing algorithms, to place virtual objects or information in the environment. The VR hardware and software then treats these objects as if they are anchored or connected to specific real-world locations or objects.

## Hardware and software requirements

This section provides an overview of both hardware and software requirements for using the Vuforia SDK with Unity.

The table below lists the supported mobile device operating system (OS) versions required for running applications created with the Vuforia SDK. The table also includes supported OS and Unity versions for developing applications with Vuforia.

### Mobile devices

| **Device OS**|  | **Development OS **|  | **Unity Version**|  |
|:---|:---|:---|:---|:---|:---| 
| Android (1)| 4.1.x+ | Windows (2) | 7+ | Windows (2) | 2017.2+ |
| iOS (2) | 9+ | OS X | 10.11+ | OS X | 2017.2+ |
| Windows (2)| 10 UWP |  |  |  |  |

1. 32-bit only 
2. 32 & 64-bit

### Optical see-through digital eyewear

The Vuforia SDK supports a range of optical see-through digital eyewear devices. The table below lists supported devices, along with their required operating system (OS) versions. The table also includes supported OS and Unity versions for developing applications with Vuforia for these devices.

| **Device**|  | **Device OS** |  | **Development OS** |  | **Unity Version** |  |
|:---|:---|:---|:---|:---|:---|:---|:---| 
| HoloLens| Current version | Android (1)(2) | 4.0.3+ | Windows (3) | 7+ | Windows (3) | 2017.2+ |
| ODG| R7+ | Windows (1) | 10 UWP | OS X | 10.11+ | OS X   | 2017.2 |
| Epson| BT-200 |  |  |  |  |  |  |

1. 32-bit only
2. 4.0.3 Native only support for Epson BT-200
3. 32 & 64-bit


## Vuforia tools

Some Vuforia tools are only supported on specific hardware. The table below lists these tools, along with their supported devices and required OS versions. 

| **App**| **Devices** | **OS Version** |
|:---|:---|:---| 
| Calibration Assistant| Moverio BT-200<br/>ODG R-7 | Android 4.0.3+ |
| Object Scanner| Samsung Galaxy S8+<br/>Samsung Galaxy S8 <br/>Samsung Galaxy S7<br/>Samsung Galaxy S6 | Latest supported OS on the device |

For more detailed information on these tools see the [Vuforia Calibration Assistant](https://library.vuforia.com/articles/Training/Vuforia-Calibration-App) and [Object Scanner](https://library.vuforia.com/articles/Training/Vuforia-Object-Scanner-Users-Guide) pages in the [Vuforia developer library](https://library.vuforia.com/).

### Virtual Reality SDK integration support

Below is a list of VR SDKs fully integrated into the Unity Editor, along with the release version of the Editor where they were first integrated.

| __VR SDK__| __Versions__ |
|:---|:---| 
| Google VR SDK| Unity  2017.2 |
| Cardboard Android SDK| Unity 2017.2 |
| Windows Mixed Reality (HoloLens only)| Unity 2017.2 |

### Graphics API support

The table below lists all the Graphics APIs supported by Vuforia when developing applications on supported operating systems.

| __Android__| __iOS__ | __Windows__ |
|:---|:---|:---| 
| OpenGL ES 2.0<br/>OpenGL ES 3.x| OpenGL ES 2.0<br/>OpenGL ES 3.x <br/>Metal (iOS 8+) | DirectX 11 on Windows 10 |

* For more information on using Vuforia with digital eyewear (such as the ODG R7+ and Epson BT-200), see Vuforia documentation on [Vuforia for digital eyewear](https://library.vuforia.com/content/vuforia-library/en/articles/Training/Vuforia-for-Digital-Eyewear.html)

* For more information on using Vuforia with HoloLens, see Vuforia documentation on [working with the Hololens sample in Unity](https://library.vuforia.com/content/vuforia-library/en/articles/Solution/Working-with-the-HoloLens-sample-in-Unity.html)

* For more information on using Vuforia with the Google VR SDK, see Vuforia documentation on [Developing for Google Cardboard](https://library.vuforia.com/content/vuforia-library/en/articles/Solution/Developing-for-Google-Cardboard.html)

## Quick start guide

This section provides instructions on setting up a Unity project with Vuforia as well as creating your first Vuforia application with Unity. Use this tutorial as a starting point for the development of your AR or MR application.

### Project setup

Setting up your project to develop Vuforia AR or MR mobile applications is very similar to the set-up process for building with Unity for a mobile platform. The Unity Installer includes the Vuforia SDK. Follow the instructions for downloading and installing Unity on the [InstallingUnity](InstallingUnity) manual page. Vuforia provides a selection of Prefabs designed to be dropped into a Scene to provide feature functionality to your application. These are all available from inside the Unity Editor.

You should adhere to the same performance considerations as required for developing regular mobile games. For information on optimising for mobile devices, see Unity documentation on [mobile optimisation](MobileOptimisation).

To get Vuforia set up with Unity:

* Install the [latest version of Unity](https://unity3d.com/get-unity/download), and in the Unity component selection section of the installer, select __Vuforia Augmented Reality Support__, along with either the __iOS Build Support__ or __Android Build Support__ packages.

![Installing Vuforia Augmented Reality support through Unity Installer](../uploads/Main/installing_vuforia.png)

**Note:** Most AR and MR applications target mobile devices, so the focus of this guide is development for Android and iOS. See guides for enabling build support for Android and iOS devices in the Getting Started documentation for [Android](android-GettingStarted) and [iOS](iphone-GettingStarted).

* Create a Vuforia developer account from the [Vuforia registration page](https://developer.vuforia.com/user/register). This account gives you access to the tools you need to make AR and MR applications with Vuforia in Unity.

* If you have not already created a Unity ID, then do so from the [Unity registration page](https://id.unity.com/en/conversations/8c075ba1-a442-41b1-b64d-ad4fb3c56073008f?view=register). You need a Unity ID to download any packages from the Unity Asset Store.

* Open Unity and create a new 3D Project (make sure the __3D__ option is selected next to the __Add Asset Package__ button). Name your Project, then click the __Create project__ button.

![Creating a new 3D project](../uploads/Main/new_project.png)

**Tip:** Download the [Vuforia AR+VR Sample package](https://www.assetstore.unity3d.com/en/#!/content/101547) from the Unity Asset Store. This package provides useful example Scenes demonstrating important features. You will not need this for following this guide, but it is useful to have for further learning later.

#### Activating Vuforia in Unity

To activate Vuforia in your Unity project, access the Player Settings from __Edit__ &gt; __Project Settings__ &gt; __Player__ and select the tab for the mobile device you are building to. Under __XR Settings__, tick the __Vuforia Augmented Reality Support__ checkbox.

![Enabling Vuforia Augmented Reality Support in Unity Player Settings](../uploads/Main/enabling_vuforia_ar_support.png)

Your Scene now contains two GameObjects: a main Camera, and a directional light. You need to add a new AR Camera to the Scene in order to enable AR functionality, and you need to delete the current __Main Camera__ GameObject from the Scene. 

To delete the Camera GameObject, select it in the __Hierarchy window__ and press the delete key on your keyboard, or right click it and select __Delete__.

#### Adding a Vuforia AR Camera and other GameObjects

To add an AR Camera to your scene, go to __GameObject__ &gt; __Vuforia__ &gt; __AR Camera__. 

If this is the first Vuforia GameObject added to your Scene then Unity also prompts to import your Vuforia Assets. Select __Import__, and Unity imports all necessary Vuforia files into your project.

The __Project window__ displays 4 new folders, one of which is called __Vuforia__. The code and Assets in this folder provide the main AR and MR functionality. The other folders provide sample Scenes, resources, tools, and plugins so that you can develop AR and MR applications for a variety of devices.

![Empty project with all imported Vuforia assets](../uploads/Main/Importing_assets.png)

Create a new folder in your project. To do this, navigate to the Project window, click the __Create__ button, and select __Folder__. Name this new folder _Scenes_ and save a [new Scene](CreatingScenes) inside this folder.

![Creating an empty folder and naming it Scenes](../uploads/Main/New_folder.png)

This process also adds a new ARCamera GameObject in your Scene hierarchy.

#### Creating a Vuforia license key

The last step in the setup process is to create a license key from the [License Manager section](https://developer.vuforia.com/Targetmanager/licenseManager/licenseListing) of the Vuforia Developer Portal. You need to enter this into Unity's Vuforia configuration settings in order to build and test your application with Unity. 

Visit the [Vuforia Developer Portal](https://developer.vuforia.com/user/login) and log in (or create a new account). Navigate to the __License Manager__ in the __Develop__ section and click the __Get Development Key__ button to open the __Add License Key__ page.

![Creating a Vuforia Development Key](../uploads/Main/creating_dev_key.png)

On the __Add License Key__ page, enter a name for your app. Accept the terms and conditions, then click the __Confirm__ button to generate a new license key.

![Confirming Vuforia development key details](../uploads/Main/vuforia_dev_key_details.png)

On the next page, agree to the Vuforia Developer conditions (tick the box) and then click the __Confirm__ button. This brings you back to the __Licence Manager__ page where you can see your newly created license in a list where its status is __Active__. Click on the name of your App to view the license details. This allows you to retrieve your development license key.

![License Manager](../uploads/Main/license_manager.png)

Copy the license key to the clipboard and navigate back to your Unity Project.

![Copying your Vuforia License key](../uploads/Main/copying_license_key.png)

Select the __ARCamera__ GameObject from the __Hierarchy window__ and, in the Inspector window, navigate to the the __Vuforia Behaviour(Script)__ component and click the __Open Vuforia configuration__ button. 

![Accessing Vuforia configuration settings](../uploads/Main/config_settings.png)

The __Inspector window__ displays a list of __Vuforia Configuration__ options. Paste your Vuforia Development key into the __App License Key__ text box under the Vuforia section and then click the __Add License__ button.

![Entering your Vuforia development key in the Vuforia Configuration settings](../uploads/Main/entering_key.png)

#### Testing your set-up

To test Vuforia apps in the Unity Editor, you need to have a webcam connected to your PC or laptop. As a final step to make sure Vuforia is now installed properly in your Unity Project, press the __Play__ button to test your Scene. If Vuforia is set up correctly, a video feed from your webcam appears in the Editor Game View. 

Now you are ready to set up Image Targets and add AR functionality to your Project.

### Setting up Image Targets

This section shows you how to set up a simple Image Target and get it responding to basic tracking events.

To allow your application to recognize images and use them as Targets to trigger gameplay, display graphics or information, you need to create a __Target database__. You can create Target databases directly from the Vuforia Developer Portal [Target Manager](https://developer.vuforia.com/Target-manager) page, as the steps in this section describe.

Log into your [Vuforia Developer account](https://developer.vuforia.com/user/login). Then navigate to the [Target Manager](https://developer.vuforia.com/Target-manager) page and click on the __Add Database__ button.

![Adding a new Target Database](../uploads/Main/add_new_target_database.png)

On the __Create Database__ page, type a name for your database, select __Device__ from the __Type__ options, then click the __Create__ button. 

![Creating a new Target Database](../uploads/Main/create_target_database.png)

This adds the new Target database to the __Target Manager__ list. Now click on the __Database name__ in the list to open the __Device Database list__.

![Managing the new Target Database](../uploads/Main/manage_database.png)

This brings you to the __Target list__ page for the database, where you can add new Targets and download the database in specific formats for use with several platforms. Click the __Add Target__ button to open the __Add Target__ popup window.

![Open Add Target window](../uploads/Main/add_target_window.png)


The __Add Target__ window presents you with options to specify details about the Target you want to add. There are four different types of [Targets](https://library.vuforia.com/articles/Solution/Targets.html) you can add: Single Image, Cuboid/Box, Cylinder and 3D Object. Under __Type__, Select __Single Image__ and browse your hard drive to locate the image you want to use as an Image Target. 

![Choosing Target Type](../uploads/Main/choose_target_type.png)

This example uses a playing card to demonstrate the Image Target recognition capabilities in Unity. 

![Image Target used ](../uploads/Main/image_target.png)

Use any image, but make sure that the image has enough detail to be rated as a 5-star Target so that the camera can easily track it. 

![Choosing Target image](../uploads/Main/choose_target_image.png)

The __Width__ value is a scale value that you need to set to the size you want the image to appear in your Unity Scene (in real-world units). Unity measures everything in your Scene in relation to the size of your Target image. For this example, the width of the playing card is 5.5cm, so you would use _5.5cm_ as the __Width__ value. If you need a larger size Target, then increase this __Width__.

![Setting a Target Width](../uploads/Main/set_target_width.png)

Enter a name for the Target image, and click the __Add__ button to upload the Image Target to the database.

![Naming the Target and adding it to the database](../uploads/Main/name_target.png)

The image appears in the list of Targets with a __Rating__ value represented by stars. If your __Rating__ is less than 5 stars, it may be harder for the camera to track it. To learn more about what affects Image Target ratings, see Vuforia documentation on [Optimizing target detection and tracking stability](https://library.vuforia.com/articles/Solution/Optimizing-Target-Detection-and-Tracking-Stability.html).

Once you are satisfied with your image's Rating, select the checkbox to the left of the __Image Target__ name and click the __Download Database__ button.

![Downloading the Target database and Target quality rating](../uploads/Main/target_rating.png)

On the __Download Database__ window, under __Select a development platform__, select __Unity Editor__, then click the __Download__ button. This downloads a Unity package of the Target database that you can save on your hard drive.

![Downloading Database Unity package](../uploads/Main/download_database_package.png)

Switch back to your Unity project to import the Unity package for use in your application.

### Importing and activating the Target Database in Unity

In the Unity Editor, navigate to __Asset__ &gt; __Import Package__ &gt; __Custom Package__ and find the package on your hard drive. In the __Import Unity Package__ window, click the __Import__ button.

Select the __ARCamera__ from the __Hierarchy window__ and, in the __Inspector window__, navigate to the __Vuforia Behaviour (Script)__ component and click on the __Open Vuforia configuration__ button. 

![Accessing Vuforia configuration settings](../uploads/Main/vuforia_config_settings.png)

In the __Vuforia Configuration__ window, under __Datasets__, select and check both the __Load [DatabaseName] Database__ and __Activate__ checkboxes. This activates your Image Target database for use with Unity.

![Activating imported Image Target database](../uploads/Main/activate_database.png)


### Adding Image Targets to your Scene

To add an Image Target to the Scene, go to __GameObject__ &gt; __Vuforia__ &gt; __Image__.

![Adding an Image Target GameObject](../uploads/Main/add_image_target_go.png)

With the Image Target GameObject in your Scene, select it and look at the __Inspector__ window to view its components.

In the __Image Target Behaviour__ component, click on the __Database__ drop-down list and select your Target database. In the __Image Target__ drop-down list, select the name of your Image Target from the database. 

![Adding a Target to the Image Target Behaviour component](../uploads/Main/adding_target_in_imagetargetscript.png)

Note: There is no need to click the __Add Target__ button, as this brings you to the Vuforia website to give you information about adding Targets to your app.

The last step is to make a 3D GameObject appear when Vuforia recognizes the Image Target.

### Displaying 3D Models on top of tracked images

This section describes how to display a GameObject when the camera recognizes and tracks an on-screen Image Target. 

Make the GameObject a child of the Image Target GameObject. This child GameObject must contain both a __MeshRenderer__ and __MeshFilter__ component. 

Add a Cube Primitive as a child to your Image Target GameObject. To do this, right-click it and select __3D Object__ &gt; __Cube__ from the pop-up menu.

![Adding a Cube Primitive as a child to the Image Target GameObject](../uploads/Main/add_cube.png)

Now scale the Cube GameObject, and move it closer to your Image Target GameObject to make it look like it is sitting on the Target image. Use the __Scene view__ to judge the position of the GameObject. If you used the same __Width__ as the playing card in this guide, then change the X, Y and Z Scales of the GameObject’s Transform component to 0.5 and change the __Transform Position__ Y value to 0.25 to make it sit well on the Image Target GameObject. 

![Changing scale and Y position of the cube GameObject](../uploads/Main/reposition_cube.png)

Your Scene should look something like this:

![Scene view of the Cube on the ImageTarget GameObject](../uploads/Main/scene_view_test.png)

Click the Unity Editor Play button to test the AR functionality. When you place the image in front of the webcam, the Cube appears on top of the image in the __Game__ view. 

![Game view showing cube displayed on track image](../uploads/Main/game_view_test.png)

The Camera component on the __ARCamera__ has its default __Far Clipping Planes__ set to 2000. For games or applications which require image tracking at larger distances (such as those requiring AR or MR glasses), you need to adjust the __Far Clipping Planes__ for the __Camera__ component in Unity, and increase the size of the Targets to ensure the device camera can easily track them.

You have now successfully made a simple app that uses an Image Target, and displays a basic 3D shape in its place once the camera can track it.

## Platform configuration settings

This section provides a step-by-step guide for configuring your Unity Project to build Vuforia Augmented/Mixed Reality applications.

Here is a list of important XR settings used in Vuforia Unity integration. To access these, open the Player Settings (__Edit__ &gt; __Project Settings__ &gt; __Player__, then select the tab for the device you are building to):

* __Vuforia Augmented Reality support__: Enables Vuforia Augmented Reality support in your application

* __Virtual Reality SDKs__: Allows Vuforia features to be integrated into VR applications. This menu is displayed when you select the Virtual Reality Supported checkbox.

![Vuforia Augmented Reality Support and Virtual Reality SDKs list in XR Settings](../uploads/Main/vuforia_ar_support.png)

Vuforia supports the following XR SDKs:

* [Google Cardboard through Google VR SDK](https://developers.google.com/vr/cardboard/overview)

* [Google Daydream through Google VR SDK](https://developers.google.com/vr/cardboard/overview)

* [Microsoft HoloLens through Windows 10 SDK](https://developer.microsoft.com/en-us/windows/mixed-reality/install_the_tools)

* [Vuforia SDK](https://library.vuforia.com/content/vuforia-library/en/articles/Best_Practices/Best-practices-for-hybrid-VRAR-experiences.html)

The __Vuforia VR SDK__ (in the __Virtual Reality SDKs__ list) is a stand-alone VR configuration with no external dependencies. It provides stereo rendering and distortion correction, along with head and hand tracking (with positional tracking available for Tango), and viewer profile support to define parameters of various VR headwear.

### Stereo rendering method

The stereo rendering method is only relevant when using the Vuforia Virtual Reality SDK. Android, iOS, and Windows Mixed Reality devices support Multi-Pass instancing, Single-Pass Instancing and non-instancing.

When using Vuforia Augmented Reality with another Virtual Reality SDK, stereo rendering support is determined by the Virtual Reality SDK being used.

### Supported graphics APIs

__Recommendation:__ In Unity's Player Settings (__Edit__ &gt; __Project Settings__ &gt; __Player__, then select the tab for the device you are building to), open __Other Settings__ and enable __Use Auto Graphics API__.


| __Android__| __iOS__ | __Windows__ |
|:---|:---|:---| 
| OpenGL ES 2.0<br/>OpenGL ES 3.x| OpenGL ES 2.0<br/>OpenGL ES 3.x <br/>Metal (iOS 8+) | DirectX 11 on Windows 10 |

### Supported features

Vuforia provides a number of features to allow development of AR/MR applications.

The table below lists these features along with the OS and device types supporting them.

| **Feature**| **Description** | **OS** | **Handhelds** | **Eyewear** |
|:---|:---|:---|:---|:---| 
| Image Targets| Tracks planar images | Android, iOS, UPW | Yes | Yes |
| Multi Targets| Tracks geometric arrangements of images | Android, iOS, UPW | Yes | Yes |
| Cylinder Targets| Tracks images wrapped on cylinders and cones | Android, iOS, UPW | Yes | Yes |
| User Defined Targets| Tracks images captured by users at runtime | Android, iOS, UPW | Yes | Not recommended |
| Cloud Recognition| Cloud-based Image Targets | Android, iOS, UPW | Yes | Yes |
| Device Tracking| 3 DoF & 6 DoF positional tracking*  | Android, iOS, UPW | Yes ( Limited to 6 DoF ) | Yes ( Limited to 6 DoF ) |
| VuMark| Customizable encodable AR markers | Android, iOS, UPW | Yes | Yes |
| Object Reco| Tracks 3D objects from scans | Android, iOS, UPW | Yes | Yes |
| Model Targets**| Track 3D objects from 3D models | Android, iOS, UPW | Yes | Yes |
| Smart Terrain| Track surfaces and geometry in the user’s environment | Android, iOS, UPW | Yes | Limited |
| AR + VR| AR feature support for VR apps | Android, iOS, UPW | Yes | Yes |

__*__ 6 degrees of freedom tracking is available for Tango and HoloLens devices

__**__ Model Targets are available through the Vuforia Early Access Program and public in Unity 2017.3

## Helpful tips

Here are a few useful tips that will reduce your learning curve when working with Vuforia in Unity.

### Image Target tracking

When a camera is tracking an Image Target in the in-Editor Play mode, Unity disables all components belonging to the Image Target GameObject’s child GameObjects. This does not include any Script components attached to the child GameObjects of the Image Target GameObject. Any Scripts continue to run even when the Image Target is not in view. This might require you to do conditional checks to prevent any code in the Script’s `Update()` method constantly running if you don't need it. Alternatively, you can disable the Script component in code, and re-enable it whenever it is needed again.

### Running code during Image Target state change events

A useful script for running code during specific Image Target tracking event states (such as whether the target is visible or not) is the __Default Trackable Event Handler (Script)__ component attached to each Image Target GameObject.

![Locating the Default Trackable Event Handler Script](../uploads/Main/default_trackable_event_handler.png)

Here are two of the most useful methods:

```
private void OnTrackingFound()
```

Unity calls this method from the __Default Trackable Event Handler (Script)__ component of the specific instance of an Image Target GameObject when Vuforia finds it in the __Camera view__. This method is very useful for running specific code at the very beginning of tracking an object (such as adding the GameObject to a list of active GameObjects).

```
private void OnTrackingLost()
``` 

Unity calls this method from the __Default Trackable Event Handler (Script)__ component of the specific instance of an Image Target GameObject when Vuforia loses track of an Image Target from the Camera view. This method is very useful for running specific code as soon as an Image Target disappears from view (such as removing the GameObject from a list in your GameManager keeping track of all GameObjects active in your application).

### Extended Tracking

For Image Targets that only require an initial setup and registration, and do not require images to be constantly tracked, navigate to the Target's __Image Target Behaviour (Script)__ component and enable the __Enable Extended Tracking__ option. 

![Enabling Extended Tracking for ImageTarget GameObject](../uploads/Main/enable_extended_tracking.png)

__Enable Extended Tracking__ allows positions and orientations of Image Targets to persist even when not in view of the Camera (after the camera has recognized them at least once) and uses features of the environment to improve tracking performance. More detailed information on Extended Tracking with Vuforia is available in the Vuforia documentation on [extended tracking](https://library.vuforia.com/articles/Training/Extended-Tracking).

### Publishing your AR/MR application

To export your Vuforia AR or MR application from Unity to mobile platforms, use the same steps as when normally publishing to Android or iOS devices. See documentation on publishing for these platforms:

* [Publishing to Android](class-PlayerSettingsAndroid)
* [Publishing to iOS](class-PlayerSettingsiOS)

No special settings are required.

### Useful links

Here are some useful resources and tutorials to help you learn more about the many features available with Vuforia.

* [Unity Vuforia forums](https://forum.unity.com/forums/vuforia.138/)

* [Vuforia Developer Forums](https://developer.vuforia.com/forum)

* Vuforia documentation: [Vuforia Developer Library](https://library.vuforia.com/)

* Vuforia documentation: [Best practices for mixed reality AR/VR experiences](https://library.vuforia.com/articles/Best_Practices/Best-practices-for-hybrid-VRAR-experiences.html)

### Troubleshooting guides

This section provides links to useful troubleshooting information for the most common problems you may encounter when developing with the Vuforia SDK.

* [Vuforia Developer Portal: FAQ]([https://developer.vuforia.com/forum/faq/faq](https://developer.vuforia.com/forum/faq/faq)