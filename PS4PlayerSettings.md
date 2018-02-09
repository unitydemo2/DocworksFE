# PS4 Player Settings 

This page details the Player Settings specific to PlayStation 4. A description of the general Unity Player Settings can be found in the [Player Settings](https://docs.unity3d.com/Manual/class-PlayerSettings.html) manual. You can use UnityEditor.PlayerSettings.PS4 class to access these settings from Editor scripts.

## Resolution and Presentation

![](../uploads/Main/PS4PlayerSettings-0.png)

| **Property:**| **Function:** |
|:---|:---| 
| __Color Depth__ | The accuracy (format) of the color output to the main screen. |
| __Base mode Resolution__| The resolution that the PS4 outputs to the main screen when running in Base mode.  |
| __Pro mode Resolution__| The resolution that the PS4 outputs to the main screen when running in PS4 Pro mode.  |
| __1080p fallback__| Drop back to using 1080p resolution if in PS4 Pro mode and the TV or monitor doesn’t support higher resolutions. |
| __VR reprojection rate__| Only valid when targeting PS VR. This is the desired frame rate cap of your title, which also defines the VR reprojection mode that is used. As a SIE’s technical requirement (TRC), your title should be able to reach this frame rate consistently. During VR mode, this property overrides the V Sync Count value found in Unity’s Quality Settings.
| Disabled | No reprojection is used. This is not TRC compliant and is intended only for testing. |
| 60Hz | Application runs at 60 frames per seconds, while VR display refreshes at 120Hz with reprojection.|
| 90Hz | Application runs at 90 frames per seconds, while VR display refreshes at 90Hz with reprojection.|
| 120Hz | Application runs at 120 frames per seconds, while VR display refreshes at 120Hz with reprojection.|

## Icon

![](../uploads/Main/PS4PlayerSettings-1.png)

| **Property:**| **Function:** |
|:---|:---| 
| __Override for PS4__| You must check this to be able to set your application icon. Having an icon is a SIE’s technical requirement. |
| __Icon slot__| This icon is the image displayed in numerous locations within the PlayStation 4 operating system, including the application icon displayed on the home screen . The format of the image must be:<br/>- 512 x 512 pixels<br/>- PNG 24-bit<br/>- Non-interlaced format |

## Splash Image

![](../uploads/Main/PS4PlayerSettings-2.png)

| **Property:**| **Function:** |
|:---|:---| 
| __Virtual Reality Splash Image__| This property is not used on the PS4 platform. |

For all other properties, please see the general [Splash Screen](https://docs.unity3d.com/Manual/class-PlayerSettingsSplashScreen.html) documentation.

## Other Settings

### Rendering

![](../uploads/Main/PS4PlayerSettings-3.png)

| **Property:**| **Function:** |
|:---|:---| 
| __Color Space__| Choose which color space should be used for rendering. The options are Gamma and Linear. See the Unity Manual page on Linear Rendering for a guide to the difference between the two. |
| __Static Batching__| Static batching allows the engine to reduce draw calls on static (non-moving) geometry. Refer to Draw Call Batching documentation for more info. |
| __Dynamic Batching__| Dynamic batching allows the engine to reduce draw calls on moving geometry. Refer to Draw Call Batching documentation for more info. |
| __Compute Skinning__| Uses GPU Compute skinning, freeing CPU resources. |
| __Graphics Jobs (Experimental)__| Graphics Jobs distribute CPU rendering activity over generic Worker Threads. This usually translates in overall better (lower) frame times for applications bound by CPU. <br/>Forward Rendering path has been parallelised more in Unity and can take better advantage of Graphic Jobs compared to the Deferred path. |
| __Graphics Jobs Mode__| |
| Legacy | Rendering work that would normally be done in the Main Thread is instead divided across Worker Threads. The output of this work is render commands that the Render Thread then consumes and turns into native (Gnm) render commands.|
| Native | Rendering work that would normally be done in the Main Thread is instead divided across Worker Threads. These Worker Threads generate the native (Gnm) render commands directly, in parallel.  Consequently, the Render Thread (called "GfxDeviceWorker") that used to run on CPU Core 1 is not needed anymore and it’s replaced by an additional generic Worker Thread. This mode is particularly beneficial for applications that otherwise would be bound by the Render Thread. |
| __Virtual Reality Supported__| Controls whether or not this title should be able to function in VR mode, either entirely or in part. |
| __Virtual Reality SDKs__| Specify which VR devices can be loaded for PS4. This list must contain ‘PlayStation VR’ to allow VR mode. <br/>At application start-up, Unity will try to automatically initialize the first SDK in the list, using default parameters. Therefore, it’s required to add ‘None’ as the first element in the list, so actual PS VR initialization can be handled from application scripts and can comply with SIE’s technical requirements. See VR Overview for more information on VR in Unity. |
| __Stereo Rendering Method__| Choose the desired stereo rendering method for PS VR.|
| Multi Pass (Slow)| Draws first the left eye and then the right eye.|
| Single Pass (Fast)| Draws both eyes at the same time. This changes the number of messages Unity sends during VR rendering and may affect Image Effects that make some assumptions on the order of events. Rendering both eyes at the same time reduces the cost of VR rendering on the Main Thread and slightly reduces it on the Render Thread.|



### Configuration

![](../uploads/Main/PS4PlayerSettings-4.png)

| **Property:**| **Function:** |
|:---|:---| 
| __Scripting Backend__| Allows you to select between IL2CPP and Mono2x scripting backends. IL2CPP often offers better runtime performance, while Mono2x allows faster iteration times during development. Also, script debugging is only available with Mono2x. |
| __Disable HW Statistics__| Disables sending statistics on the hardware your title is being ran on back to Unity. Note that this is always disabled on PS4, to comply with SIE’s technical requirements. |
| __Mono environment variables__| Allows you to set additional environment variables for the mono runtime. Write it in the format `key=value` (for example `MONO_LOG_LEVEL=debug`). You can retrieve environment variables at runtime by calling `System.Environment.GetEnvironmentVariable`. Note that using `System.Environment.SetEnvironmentVariable` at runtime is not supported on PS4. If you leave this field empty, the application will run with the following variables: <br/>MONO_XMLSERIALIZER_THS=no<br/>MONO_REFLECTION_SERIALIZER=yes<br/>XDG_CONFIG_HOME=/app0/media/StreamingAssets |
| __PlayerPrefs support__| Enables PlayerPrefs support in your title, using the Save Data Memory API. Disable this to avoid Unity performing any initialization or other operations with the Save Data Memory api (needed in case you have custom code using the API). <br/>For more info on saving data, check the [PS4 Saving Data and DLC](PS4SavingDataAndDLC) documentation. |
| __Save Data Image__| 228 x 128  pixels, 24bit PNG, Non-interlaced. This mandatory image is displayed to users when managing game saves in the PS4 operative system, when those save games were created using the Save Data Memory API (for example, when saving PlayerPrefs). |
| __Base Mode/Pro Mode Garlic Heap Size__| These sliders let you control the ratio between the PS4’s two memory types, called Garlic and Onion. Size of Garlic memory is fixed at the value specified here, while Onion memory will progressively grow and shrink as needed by the title, using the memory available after Garlic memory reservation. Note that extreme values may have undesirable consequences on your project, so please use this with caution, and constantly assess what is appropriate in the context of your specific title. Refer to the [PS4 Memory](PS4Memory.html) documentation for more details. |
| __PS4 SDK Override__| Allows you to specify an SDK path different to the one currently active in your system environment variables. |
| __Audio Backend__| Choose between using Unity’s default AudioOut, or the more resource intensive AudioOut3d backend. AudioOut3d is only available for PS VR applications. It enables 3d sound through the headphones connected to the PS VR device. |
| __Restricted audio usage rights__| Enable audio output restrictions regarding usage rights. This checkbox enables the sdk `SCE_AUDIO_OUT_PARAM_ATTR_RESTRICTED` flag, which stops all title audio from being included in systems with a possibility of being distributed to the general public (for example PS4 shared videos). |
| __Social Screen Support__| In PS VR, allows you to show a view on the main screen attached to the PS4, different than the view currently being rendered in the HMD. `UnityEngine.VR.VRSettings.showDeviceView` is used to toggle this view at runtime. When unchecked, or when `UnityEngine.VR.VRSettings.showDeviceView` is true, the HMD view (without lens distortion) is displayed on the main screen. Note that video recording via the PS4 sharing system is disabled if you select this option. This is due a limitation on the SDK’s SocialScreen library. |
| __Scripting Define Symbols__| Use this to set custom compilation flags (see the platform dependent compilation page for more details). |

### Optimization

![](../uploads/Main/PS4PlayerSettings-5.png)

| **Property:**| **Function:** |
|:---|:---| 
| __Api Compatibility Level__| |
|.NET 2.0 | This is close to the full .NET 2.0 API and offers the best compatibility with pre-existing .NET code. Application’s build size and startup time may be higher.|
|.NET 2.0 Subset | This is close to the Mono "monotouch" profile. The advantage of using this profile is reduced build size (and startup time) but this comes at the expense of compatibility with existing .NET code. Note that .Net 2.0 subset has limited compatibility with other libraries. More information can be found here: http://docs.xamarin.com/guides/ios/advanced_topics/limitations/ |
| __Prebake Collision Meshes__| Should collision data be added to meshes at build time? |
| __Preload Shaders__| Should shaders be loaded when the player starts up? |
| __Preloaded Assets__| An array of assets to be loaded when the player starts up. |
| __AOT Compilation Options__| Allows you to set compilation options for the mono Ahead Of Time compiler. |
| __Stripping Level__| Options to strip out scripting features to reduce built player size (This setting is only available with the Mono2x scripting backend.) |
| __Strip Engine Code__| Enable code stripping. (This setting is only available with the IL2CPP scripting backend.) |
| __Vertex Compression__| Select which vertex channels should be compressed. Compression can save memory and bandwidth but precision will be lower. |
| __Optimize Mesh Data__| Remove any data from meshes that is not required by the material applied to them (tangents, normals, colors, UV). |

### Logging

![](../uploads/Main/PS4PlayerSettings-6.png)

| **Property:**| **Function:** |
|:---|:---| 
| __Logging__| Enable different logging types (see the StackTraceLogType page for details). |



## Publishing Settings

### Param File

This section allows you to set the most commonly used fields of the [Param File](https://ps4.siedev.net/resources/documents/Misc/current/Param_File_Editor-Users_Guide/0001.html#__document_toc_00000000) within Unity.  For more documentation on individual Param File properties please refer to the [Param Description File (*.sfx) Specifications](https://ps4.siedev.net/resources/documents/Misc/current/Param_File_Editor-Users_Guide/0004.html) and the [Param File Editor Features](https://ps4.siedev.net/resources/documents/Misc/current/Param_File_Editor-Users_Guide/0003.html).

Note that you can specify a full, custom Param File for your project. See the Select Param File property below.

![](../uploads/Main/PS4PlayerSettings-7.png)

| **Property:**| **Function:** |
|:---|:---| 
| __Category__| Select whether you want to build a regular PS4 application, a patch to an already-released PS4 application, or a Remaster version of an application. Refer to the Patch and Remaster Overview for details on these categories. |
| __Master Version__| The Master Version is the submission version of a product. For first release this should always be "01.00". For patch releases this should be incremented, i.e. “01.01”, “01.02”, etc. |
| __Content ID__| Packages are identified by IDs called Content IDs. See the Content ID documentation for details. |
| __User-defined parameter (1-4)__| User-defined application specific data, accessed from scripts by UnityEngine.PS4.Utility.GetApplicationParameter(*).
Refer to USER_DEFINED_PARAM_X in Param Description File (*.sfx) Specifications for more details. |
| __Parental Level (0 - 11)__| Set the parental lock level (0 - 11). The lower the number, the tighter the restriction. Check the related R4005 Technical Requirement for details. |
| __RemotePlay Key Assign__| This represents the key assign pattern used for remote play with PlayStation®Vita systems. For details on key assign patterns, refer to the Remoteplay Library Overview document. |
| __RemotePlay Mapping Folder__| The folder that contains the replacement key mapping images for Remoteplay. The contents of this folder must match the structure of the keymap_rp folder as described in the Remoteplay Library Overview documentation. |
| __Enter Button Assignment__| Choice of controller button to be used as enter (Circle button or Cross button). Used for user input on the the OS common dialogs. Find more info at the Programming Start-up Guide. |
| __User Management__| Leaving this flag unchecked activates the InitialUserAlwaysLoggedIn mode, as described in the User Management documentation. |
| __PlayStation®Move Support__| This indicates whether "PlayStation®Move Safety Notice" is displayed in the option menu or not. |
| __Stereoscopic 3D Support__| Enable Stereoscopic 3D support. See the Stereoscopic 3D Parameter documentation for more info. |
| __Share Menu__| Check to enable the custom Share Menu feature. See the Share Menu Parameter documentation for more info. |
| __Exclusive VR__| Select this when the Application runs exclusively on VR mode. This property is related to the Exclusive VR flag in the “ATTRIBUTE” section of the Param file. Note that the “Virtual Reality Supported” checkbox, also found in Player Settings, is used to set the other two possible values of said Param file attribute (VR not supported and non-exclusive VR). |
| __CPU mode__| Set the CPU mode. The default and recommended value is 7CPU mode. 6CPU usually has no advantages and may cause problems. |
| __Persistent Data Size__| The size in MB of the download0 mountpoint (accessible via Application.persistentDataPath on PS4). Specify the required Amount of HDD space to allocate during installation for persistent data (Download Data). This property cannot be set higher than 1024, to comply with SIE’s technical requirements. |
| __Enable Play Together__| Enable Play Together. |
| __Max Player Count__| Enter the maximum number of users for joining Play Together (2 to 8). |
| __Video Recording Used__| Check to enable VideoRecording library. See the VideoRecording Parameter documentation for more info. |
| __Content Search Used__| Check to enable ContentSearch library. See the Content Search Parameter documentation for more info. |
| __PS VR IPD distance__| For PS VR, indicate what eye to eye distance setting should be used: per user, system default, or to allow both. System default value is 63mm. |
| __Select Param File__| The location of your self-made param.sfx file. If a file is specified here, then its contents will override all of the above Param File settings. This can be useful if you plan to submit your application in multiple territories which require slightly different parameters. More information about creating parameter files at the Param File Editor User’s Guide and the Publishing Tools Overview. |

### Modules

![](../uploads/Main/PS4PlayerSettings-8.png)

| **Property:**| **Function:** |
|:---|:---| 
| __Modules__| List of PS4 SDK PRX modules to include in the build. Removing required modules from this list will stop the title from working, whilst removing non-required modules will make the final package smaller. When updating to a new SDK version you might require to use the Restore button to keep the list of PRX files up to date. |

### Package

![](../uploads/Main/PS4PlayerSettings-9.png)

| **Property:**| **Function:** |
|:---|:---| 
| __Application Type__| The application type, set in submission materials. See Product and Package documentation for more info. |
| __Pass-code (32 chars)__| A pass-code used for packaging your project. A random pass-code is generated if none is entered. You can use this pass-code along with the SDK Publishing Tools to unpackage an installable build file, as documented here. |
| __Background Image__| 1920x1080 pixels, 24bit PNG. This optional file is an image file that displays as the background for the Content Info Screen of the application. |
| __Start-up Image__| 1920x1080 pixels, 24bit PNG. This mandatory splash image is displayed by the PlayStation 4 when the title is first launched. It continues to display until Unity has loaded scene 0. |
| __Disable Start-up Auto-Hide__| Prevent the runtime from automatically hiding the start-up image. Enable this checkbox if you want fine control on when the image should be hidden, rather than letting Unity hide it automatically. Use PS4.Utility.HideStartupImage() method to hide the image manually. |
| __Background Audio__| This optional ATRAC9 audio resource starts playback when the focus in the home screen is on the application and the down button is pressed to display the screen labeled "Overview".  |
| __Share parameter file__| Mandatory JSON file that configures how the SHARE button operates. It should be created with the Share File Editor. |
| __Share overlay Image__| This optional png image is overlayed on top of any shared video. For details see the Share File Editor documentation. |
| __Share privacy guard Image__| 64x16 pixels, 24bit PNG. When sharing gameplay videos from the PlayStation 4, certain system events (such as messages, invites, etc.) are automatically hidden by the operating system with a black box, or an image specified here. Requires GameLiveStreaming native plugin. See GameLiveStreaming System Overview for details. |

### Title Voice Recognition Details

![](../uploads/Main/PS4PlayerSettings-10.png)

| **Property:**| **Function:** |
|:---|:---| 
| __pronunciation.xml__| This mandatory file allows your title to be selected by voice recognition. Use PSVR Dictionary Tool to create it. |
| __pronunciation.sig__| This mandatory file allows your title to be selected by voice recognition. Use PSVR Dictionary Tool to create it. |



### PlayStation Network

![](../uploads/Main/PS4PlayerSettings-11.png)

| **Property:**| **Function:** |
|:---|:---| 
| __Trophy Pack (trophy.trp)__| Specify the location of your trophy pack file (*.trp). Note that you must set the NP Communications ID in Player Settings and that must match the NP Communications ID specified in the trophy pack. The Trophy Pack File Utility can be used to create and modify your trophy pack. |
| __NP Title ID (nptitle.dat)__| The identifying file unique and specific to your title. This file is mandatory if you intend to publish a title using NP features. This is only acquired through DevNet. |
| __NP Age Rating (1-99) or 0 for no Age Rating__| The age rating required to use network features. See related R4109 Technical Requirement for more info. This value can be overridden from script when initializing the NpToolkit2 plugin, for example if you need to specify a rating per region.  |
| __NP Title Secret__| The secret key required to access network functionality. This is granted to you through DevNet. |
| __Session__| Enable Sessions Push Notifications. Not used by the NpToolkit2 plugin. |
| __Presences__| Enable Presence Push Notifications. Not used by the NpToolkit2 plugin. |
| __Friends__| Enable Friends Push Notifications. Not used by the NpToolkit2 plugin. |
| __Game Custom Data__| Enable Game Custom Data Push Notifications. Not used by the NpToolkit2 plugin. |

----

* <span class="page-edit">2017-05-15  <!-- include IncludeTextNewPageNoEdit --></span>




