#Android Player Settings

This page details the __Player Settings__ specific to Android. A description of the general Player Settings can be found [here](class-PlayerSettings).

##Resolution And Presentation

![](../uploads/Main/PlayerSetAndroidResPres.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|**Orientation** ||
|__Default Orientation__ |The game's screen orientation. The options are **Portrait** (home button at the bottom), **Portrait Upside Down** (home button at the top, Android 2.3+), **Landscape Left** (home button on the right side) and **Landscape Right** (home button on the left side, Android 2.3+).|
|**Allowed Orientations for Auto Rotation** ||
|**Allowed Orientations for Auto Rotation** |(Only visible when the _Default Orientation_ is set to _Auto Rotation_.)|
|__Portrait__ |Allow portrait orientation. |
|__Portrait Upside Down__ |Allow portrait upside down orientation.|
|__Landscape Right__ |Allow landscape right orientation (ie, home button on the **left** side). |
|__Landscape Left__ |Allow landscape left orientation (home button is on the **right** side).|
|**Other** ||
|__Use 32-bit Display Buffer__ |Specifies if Display Buffer should be created to hold 32-bit color values (16-bit by default). Use it if you see banding, or need alpha in your ImageEffects, as they will create RTs in same format as Display Buffer. Not supported on devices running pre-Gingerbread OS (will be forced to 16-bit).|
|__Disable Depth and Stencil__ |Should the depth and stencil buffers be disabled? |
|__Show Loading Indicator__ |The type of loading progress indicator that should be shown. Options are **Don't Show**, **Large**, **Inversed Large**, **Small** and **Inversed Small**. |


##Icon

![](../uploads/Main/PlayerSetAndroidIcon.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Override for Android__ |Check if you want to override the default icon with a custom one for Android. The icon images at various different sizes can be dragged into the appropriate squares. |
|__Enable Android Banner__ |Enables a custom banner for Android T.V builds |


##Splash Image

![](../uploads/Main/PlayerSetAndroidSplash.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Virtual Reality Splash Screen (Pro-only feature)__|Specifies the texture that should be used for the Android splash screen on a Virtual Reality Application.|
|__Android Splash Screen (Pro-only feature)__|Specifies the texture that should be used for the Android splash screen. The standard size for the splash screen image is 320x480.|
|__Splash Scaling__ |Specifies how the splash image will be scaled to fit the device's screen. The options are **Center (only scale down)**, **Scale to Fit (letter-boxed)** and **Scale to Fill (cropped)**.|

See also [Unity Splash Screen](class-PlayerSettingsSplashScreen) settings.


##Other Settings

![](../uploads/Main/PlayerSetAndroidOther.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|**Rendering** ||
|__Rendering Path__ |The [rendering path](RenderingPaths) enabled for the game. |
|__Automatic Graphics API__ | Allows you to select which graphics API is used. When checked, Unity will include Metal, and GLES2 as a fallback for devices where Metal is not supported. When unchecked, you can manually pick and reorder the graphics APIs. Manually picking just one API will adjust your app's info.plist which will result in appropriate app store restrictions.|
|__Multithreaded Rendering__ | Enables multithreaded rendering.|
|__Static Batching__ |Set this to use Static batching on your build (enabled by default). |
|__Dynamic Batching__ |Set this to use Dynamic Batching on your build (enabled by default). |
|__GPU Skinning__ |Should DX11/ES3 GPU skinning be enabled? |
|__Virtual Reality Supported__ |Enable this if your application is a virtual reality application.|
|__Protect Graphics Memory__ |Enable this to force the graphics buffer to be displayed only through a hardware-protected path. |

|**Identification** ||
|__Bundle Identifier__ |The string used in your provisioning certificate from your Apple Developer Network account(This is shared between iOS and Android) |
|__Version*__ |Specifies the build version number of the bundle, which identifies an iteration (released or unreleased) of the bundle. The version is specified in the common format of a string containing numbers separated by dots (eg, 4.3.2). (This is shared between iOS and Android.) |
|__Bundle Version Code__ |An internal version number. This number is used only to determine whether one version is more recent than another, with higher numbers indicating more recent versions. This is not the version number shown to users; that number is set by the versionName attribute. The value must be set as an integer, such as "100". You can define it however you want, as long as each successive version has a higher number. For example, it could be a build number. Or you could translate a version number in "x.y" format to an integer by encoding the "x" and "y" separately in the lower and upper 16 bits. Or you could simply increase the number by one each time a new version is released.|
|__Minimum API Level__|Minimum API version required to support the build.|

|**Configuration** |
|__Scripting Backend__ |Allows you to select between IL2CPP and Mono2x scripting backends. The default is Mono2x.|
|__Disable HW Statistics__|By default, Unity Android apps send anonymous HW statistics to Unity so we can provide you with aggregated information to help you make decisions as a developer. These stats can be found at (http://stats.unity3d.com/)[http://stats.unity3d.com/]. Checking this option disables the sending of these statistics for your app.|
|__Device Filter__ |Limit the game to run only on specific CPUs. |
|__Install Location__ |Specifies application install location on the device (for detailed information, please refer to http://developer.android.com/guide/appendix/install-location.html).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Automatic__ |Let OS decide. User will be able to move the app back and forth.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Prefer External__ |Install app to external storage (SD-Card) if possible. OS does not guarantee that will be possible; if not, the app will be installed to internal memory.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Force Internal__ |Force app to be installed into internal memory. User will be unable to move the app to external storage.|
|__Internet Access__ |When set to Require, will enable networking permissions even if your scripts are not using this. Automatically enabled for development builds.|
|__Write Access__ |When set to External (SDCard), will enable write access to external storage such as the SD-Card. Automatically enabled for development builds.|
|__Android TV Compatibility__ |If enabled, checks the game for Android T.V compatibility.|
|__Android Game__ |If enabled, built APK will be marked as a game rather than a regular app.|
|__Android Gamepad Support Level__ |This allows you to define the level of support your application allows for a gamepad. The options are **Works with D - Pad**, **Supports Gamepad** and **Requires Gamepad**.|
|__Scripting Define Symbols__|Custom compilation flags (see the [platform dependent compilation](PlatformDependentCompilation) page for details).|
|**Optimization** ||
|__Api Compatibility Level__ |Specifies active .NET API profile. See below.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__.Net 2.0__ |.Net 2.0 libraries. Maximum .net compatibility, biggest file sizes|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__.Net 2.0 Subset__ |Subset of full .net compatibility, smaller file sizes|
|__Prebake Collision Meshes__|Should collision data be added to meshes at build time? |
|__Preload Shaders__|Should shaders be loaded when the player starts up? |
|__Preloaded Assets__|An array of assets to be loaded when the player starts up. |
|__Stripping Level__ |Options to strip out scripting features to reduce built player size (This setting is shared between iOS and Android Platforms, and is available with the Mono scripting backend only.)|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Disabled__ |No reduction is done.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Strip Assemblies__ |Level 1 size reduction.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Strip ByteCode (iOS only)__ |Level 2 size reduction (includes reductions from Level 1).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Use micro mscorlib__ |Level 3 size reduction (includes reductions from Levels 1 and 2).|
|__Strip Engine Code__ |Enable code stripping. (This setting is only available with the IL2CPP scripting backend.)|
|__Enable Internal profiler__|Enable this if you want to get feedback from your device while testing your projects. So adb logcat prints logs from the device to the console (only available in development builds).|
|__Vertex Compression__|Select which vertex channels should be compressed. Compression can save memory and bandwidth but precision will be lower.|
|__Optimize Mesh Data__|Remove any data from meshes that is not required by the material applied to them (tangents, normals, colors, UV).|

|**Logging** | Enable different logging types (see the [StackTraceLogType](ScriptRef:StackTraceLogType.html) page for details). |



###API Compatibility Level

You can choose your mono api compatibility level for all targets. Sometimes a 3rd party .net dll will use things that are outside of the .net compatibility level that you would like to use. In order to understand what is going on in such cases, and how to best fix it, get "Reflector" on windows. 

1. Drag the .net assemblies for the api compatilibity level in question into reflector. You can find these in Frameworks/Mono/lib/mono/YOURSUBSET/
1. Also drag in your 3rd party assembly.
1. Right click your 3rd party assembly, and select "Analyze".
1. In the analysis report, inspect the "Depends on" section. Anything that the 3rd party assembly depends on, but is not available in the .net compatibility level of your choice will be highlighted in red there.



##Publishing Settings

![](../uploads/Main/PlayerSetAndroidPublish.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|**Keystore** ||
|__Use Existing Keystore / Create New Keystore__|Use this to choose whether to create a new Keystore or use an existing one. You can use the **Browse Keystore** button to select a Keystore from the filesystem. |
|__Keystore password__ |Password for the Keystore.|
|__Confirm password__ |Password confirmation (only enabled if the Create New Keystore option is chosen).|
|**Key** ||
|__Alias__ |Key alias. |
|__Password__ |Password for key alias. |
|__Split Application Binary__|Flag to split the application into expansion files. Useful only with Google Play Store when the finished build exceeds 50MB.|

Note that for security reasons, Unity will save neither the keystore password nor the key password. Also, note that the signing must be done from Unity's player settings - using jarsigner will not work. The unsigned debug keystore is located by default at `~/.android/debug.keystore` on OS X and `%USERPROFILE%\.android\debug.keystore` on Windows.


##Details

###Bundle Identifier

The __Bundle Identifier__ string is the unique name of your application when published to the Android Market and installed on the device. The basic structure of the identifier is __com.CompanyName.GameName__, and can be chosen arbitrarily. In Unity this field is shared with the iOS Player Settings for convenience.

###Stripping Level

Most games don't use all the functionality of the provided dlls. With this option, you can strip out unused parts to reduce the size of the built player on Android devices.
