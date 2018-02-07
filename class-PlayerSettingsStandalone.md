#Standalone Player Settings

This page details the __Player Settings__ specific to standalone platforms (Mac OSX, Windows and Linux). A description of the general Player Settings can be found [here](class-PlayerSettings).

##Resolution And Presentation

![](../uploads/Main/PlayerSetPCResPresNew.png)

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Resolution__ ||
|__Default is Full Screen__ |Check this box to make the game start in fullscreen mode by default. |
|__Default Is Native Resolution__ |Check this box to make the game use the default resolution used on the target machine.|
|__Default Screen Width__ |Default width of the game screen in pixels.|
|__Default Screen Height__ |Default height of the game screen in pixels.|
|__Mac Retina Support__ | Check this box to enable support for high DPI (Retina) screens on a Mac. Unity enables this by default. This enhances Projects on a Retina display, but it is somewhat resource-intensive when active.|
|__Run in background__ |Check this box to make the game keep running (rather than pausing) if the app loses focus. |
|__Standalone Player Options__||
|__Capture Single Screen__ |Check this box to ensure standalone games in fullscreen mode do not darken the secondary monitor in multi-monitor setups. This is not supported on Mac OS X.|
|__Display Resolution Dialog__ |Choose whether the game should start with a dialog to let the user choose the screen resolution. The options are __Disabled__, __Enabled__ and __Hidden by Default__ (i.e. the option only appears if the alt key is held down at startup). |
|__Use Player Log__ |Check this box to write a log file with debugging information. If you plan to submit your application to the Mac App Store, leave this option un-ticked. Ticked is the default. |
|__Resizable Window__ |Check this box to allow the user to resize the standalone player window. |
|__Mac App Store Validation__ |Check this box to enable receipt validation for the Mac App Store. |
|__Mac Fullscreen Mode__ |Choose how fullscreen mode operate on MacOSX. The options are __Capture Display__ (i.e. Unity takes over the whole display and the user cannot switch apps until fullscreen mode is exited), __Fullscreen Window__ and __Fullscreen Window with Menu Bar and Dock__. |
|__D3D11 FullScreen Mode__ |Choose the fullscreen mode when using DirectX 11.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Exclusive Mode__ |Sets the Default Fullscreen mode to encompass the whole screen without a window surrounding it.|
|&#160;&#160;&#160;&#160;__Fullscreen Window__ |Keeps the game in a window when in fullscreen. Better for allowing the game to run in the background.|
|__Visible in Background__ |Check this box to show the application in the background if Fullscreen Windowed mode is used (in Windows).|
|__Force Single Instance__ |Check this box to restrict standalone players to a single concurrent running instance.|
|__Supported Aspect Ratios__ |Choose the aspect ratios that appear in the Resolution Dialog at startup (as long as they are supported by the user's monitor). |


##Icon

![](../uploads/Main/PlayerSetPCIcon.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Override for Standalone__ |Check this box to assign a custom icon to be used for your standalone game. Upload different sizes of the icon to fit each of the squares below the checkbox.|


##Splash Image

![](../uploads/Main/PlayerSetPCSplash.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Config Dialog Banner__ |Add a custom splash image to be displayed in the __Display Resolution Dialog__.|
|__Show Unity Splash Screen__ |Shows the "Made with Unity" Splash Screen when the game is loading .|


##Other Settings

![](../uploads/Main/PlayerSetPCOther.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Rendering__ ||
|__Color Space__|Choose which color space should be used for rendering. The options are __Gamma__ and __Linear__. See the Unity Manual page on [Linear Rendering](LinearLighting) for a guide to the difference between the two.|
|__Auto Graphics API for Windows__|Check this box to use the best Graphics API on the Windows machine the game is running on. Uncheck it to add and remove supported Graphics APIs. |
|__Auto Graphics API for Mac__|Check this box to use the best Graphics API on the Mac the game is running on. Uncheck it to add and remove supported Graphics APIs. |
|__Auto Graphics API for Linux__|Check this box to use the best Graphics API on the Linux machine it runs on. Uncheck it to add and remove supported Graphics APIs. |
|__Static Batching__ |Check this box to use Static batching.|
|__Dynamic Batching__ |Check this box to use Dynamic Batching (activated by default). |
|__GPU Skinning__ |Check this box to enable DX11/ES3 GPU skinning. |
|__Graphics Jobs (Experimental)__ |Check this box to instruct Unity to offload graphics tasks (render loops) to worker threads running on other CPU cores. This is intended to reduce the time spent in `Camera.Render` on the main thread, which is often a bottleneck. **Please note that this feature is experimental**. it may not deliver a performance improvement for your project, and may introduce new crashes. |
|__Virtual Reality Supported__ |Check this box when building a Virtual Reality application. See [VR Overview](http://docs.unity3d.com/Manual/VROverview.html) for more information.|
|__Configuration__||
|__Scripting Backend__ |__Mono2x__ is the only scripting backend supported on Standalone platforms. |
|__Disable HW Statistics__ |Check this box to instruct the application not to send information about the hardware to Unity (See the [Unity Hardware Statistics](http://hwstats.unity3d.com/) page for more details).|
|__Scripting Define Symbols__|use this to set custom compilation flags (see the [platform dependent compilation](PlatformDependentCompilation) page for more details).|
|__Optimization__||
|__API Compatibility Level__ |There are two options for API compatibility level: __.Net 2.0__, or __.Net 2.0 Subset__.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__.Net 2.0__ |.Net 2.0 libraries. Maximum .net compatibility, biggest file sizes.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__.Net 2.0 Subset__ |Subset of full .net compatibility, smaller file sizes.|
|__Prebake Collision Meshes__|Check this box to add collision data to meshes at build time. |
|__Preload Shaders__|Check this box to load shaders when the player starts up. |
|__Preloaded Assets__|Set an array of assets to be loaded when the player starts up.
|__Vertex Compression__|Vertex compression can be set per channel. You can, for instance, choose to have compression enabled for everything except positions and lightmap UVs. Whole mesh compression set per imported object will override the vertex compression on objects that have it set, while everything else will obey the vertex compression options/channels set here. |
|__Optimize Mesh Data__|Check this box to remove any data from meshes that is not required by the material applied to them (e.g. tangents, normals, colors, UV).|

###API Compatibility Level

You can choose your mono API compatibility level for all targets. Sometimes a 3rd-party .net dll will use things that are outside of the .net compatibility level that you would like to use. In order to understand what is going on in such cases, and how to best fix it, install "Reflector" for Windows. 

1. Drag the .net assemblies for the API compatilibity level in question into Reflector. You can find these in __Frameworks/Mono/lib/mono/YOURSUBSET/__
1. Drag in your 3rd-party assembly.
1. Right-click your 3rd-party assembly and select "Analyze".
1. In the analysis report, inspect the "Depends on" section. Anything that the 3rd-party assembly depends on, but that is not available in the .net compatibility level of your choice, will be highlighted in red there.


##Details

###Customizing your Resolution Dialog


![The Resolution Dialog, presented to end-users](../uploads/Main/Resolution-GameLauncher.png) 

You have the option of adding a custom banner image to the Screen Resolution Dialog in the Standalone Player. The maximum image size is 432 x 163 pixels. The image does not scale up to fit the screen selector, it is automatically centered and cropped.

###Publishing to the Mac App Store

The property __Use Player Log__ enables writing a log file with debugging information. This is useful for investigating problems with your game. However you need to disable this when publishing games for Apple's Mac App Store, as Apple may reject your submission if it is enabled. See the Unity Manual [Log Files](LogFiles) page for further information about log files.

The property __Use Mac App Store Validation__ enables receipt validation for the Mac App Store. If this is enabled, your game will only run when it contains a valid receipt from the Mac App Store. Use this when submitting games to Apple for publishing on the App Store. This prevents people from running the game on a different computer to the one it was purchased on. Note that this feature does not implement any strong copy protection. In particular, any potential crack against one Unity game would work against any other Unity content. For this reason, it is recommended that you implement your own receipt validation code on top of this, using Unity's plugin feature. However, since Apple requires plugin validation to initially happen before showing the screen setup dialog, you should still enable this check, or Apple might reject your submission.

---
* <span class="page-edit"> 2017-09-04  <!-- include IncludeTextAmendPageSomeEdit --></span><br/>
* <span class="page-history"> 2017-09-04 > Added MacOS Retina Support checkbox Added in [2017.2](https://docs.unity3d.com/2017.2/Documentation/Manual/30_search.html?q=newin20172) <span class="search-words">NewIn20171</span></span><br/>




