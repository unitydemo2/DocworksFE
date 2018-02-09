# Building games for Apple TV

This manual page is primarily aimed at helping developers transition from iOS to tvOS. The Apple TV platform (also known as tvOS) builds on the foundation of the iOS platform while creating new paradigms and challenges for game developers. Deploying an existing mobile game on tvOS is just one click away, but game content often needs to be adapted to work correctly with Unity's new input controls and the fact that the game is displayed on a big screen.

## Prerequisites 
To develop for tvOS you need the following:

* A 4th generation Apple TV device (you also need a USB C &lt;-&gt; USB 3.0 cable, which is not included with the consumer package).
* Xcode 7.1 or later.
* You need to set up provisioning for this device in the same way as for iOS devices. It is recommended to create an empty tvOS app with Xcode to test that provisioning works correctly.


## Points to note before starting

* Many iOS plugins aren't compatible with Apple TV, because it only supports a subset of the iOS framework. It's recommended that you create a separate branch or copy of your game and do porting to Apple TV there. Reach out to plugin providers to ask them to update incompatible plugins.
* If your game uses more than 200 MB on disk, you should break it into smaller parts and use __On Demand Resources__. For On Demand Resources support in Unity please refer to the [_On Demand Resources_](#OnDemandResources) section below. Note that Bitcode is included with tvOS builds, which adds ~130 MB to your executables. This added size is not accounted for in distribution size, as it is be stripped by App Store servers. You can estimate Bitcode size by analyzing LLVM sections in your executable from the command line with `otool -l`. 

## Implementing input
The Apple TV Remote (Siri Remote) serves as a multi-purpose input device, working both as a traditional menu navigation controller, game controller, gyro and acceleration sensor, and as a touch gesture device. Apple TV Remote input is minimally processed by Unity and mostly routed to corresponding Unity APIs.

Usually, each game needs slight adjustment of its input scheme to leverage unique Apple TV Remote input features. Some games would benefit from treating it as a traditional game controller, with one analog axis and an extra action button, while others would benefit from using the accelerometer (for example, for steering purposes). It is recommended that you experiment with various schemes when porting a game to tvOS. 

Here are some technical details on accessing specific TV Remote features:

* If you have not yet added Made For iOS (MFi) Game Controller support to your game, see the dedicated [MFi Game Controller](iphone-joystick) page. Use the mappings listed there while setting up your custom action mappings in the Unity Editor (Edit &gt; Project Settings &gt; Input**).
* The Apple TV Remote touch area is mapped both to `Input.touches` (`Touch.type` is set to `Indirect` and is ignored by the Unity GUI), and the usual Joystick Input API (e.g. `Input.GetAxis("Horizontal");` )
* The Apple TV Remote acceleration and gyroscope are mapped accordingly to `Input.acceleration` and `Input.gyro`. `Input.acceleration` internally is derived from gyroscope API and might have some instabilities. Unfortunately there is no dedicated accelerometer API in the tvOS SDK. `Input.gyro.attitude` is derived from the gravity vector, and thus lacks rotation around the axis parallel to the gravity vector. The same applies for `Input.gyro.rotationRate`.
* The Pause/Play button on the remote is mapped to button "X" (which is then mapped to [joystick button 15](iphone-joystick)).
* The Apple TV Remote touch area click is mapped to button "A" (which is then mapped to [joystick button 14](iphone-joystick)).
* The Menu button has special behavior on this device; a long press invokes the tvOS task switcher. This behavior cannot be overridden. Short taps can be processed two ways:
    * **a)** Returning to the tvOS system home screen (if `UnityEngine.Apple.TV.Remote.allowExitToHome` is **true**)
    * **b)** Letting your app respond to taps (mapped to button "Pause" / [joystick button 0](iphone-joystick)), when `UnityEngine.Apple.TV.Remote.allowExitToHome` is **false**. This the default behavior.
    * Your app should switch between **a)** and **b)** based on the current state of your game. If the user is interacting with the top menu, enable behavior **a)**; if they are interacting in real time with the game you should enable behaviour **b)** and invoke in the in-game pause menu when this button is pressed.
* The Apple TV Remote also generates directional pad up/down/left/right button presses when you swipe to the edge of the remote. Refer to the manual page for [iOS Game Controllers](iphone-joystick) for the mappings.
* The Apple TV Remote operational modes can be controlled via a dedicated API:
    * `UnityEngine.Apple.TV.Remote.allowExitToHome`
    * `UnityEngine.Apple.TV.Remote.allowRemoteRotation`
    * `UnityEngine.Apple.TV.Remote.reportAbsoluteDpadValues`
    * `UnityEngine.Apple.TV.Remote.touchesEnabled`
* Two further wireless Made For iOS (MFi) game controllers may be connected to an Apple TV device, effectively turning it into game console. Your game may use them in the same way as iOS MFi controllers (as mentioned above), though your game should be still playbable with the Apple TV Remote alone. Currently, the number of additional controllers is limited to two; this is a documented tvOS system limitation. 

**Warning:** due to the Apple TV Remote "Menu" button being reported as [joystick button 0](iphone-joystick) when `UnityEngine.Apple.TV.Remote.allowExitToHome` is set to **false**, and the default Input Manager binding "Submit" virtual button being mapped to the same [joystick button 0](iphone-joystick), this button triggers actions on UI elements when pressing the "Menu" button. To work around this issue, remove or modify the "Submit" virtual button bindings in the [Input Manager](ConventionalGameInput).

## Setting up Unity GUI navigation via Apple TV Remote
* Open the [Input Manager](ConventionalGameInput) in the Unity Editor. Find the first occurrence of the "Submit" virtual input, expand it and change its "Alt Positive Button" to "joystick button 14".
* Select the EventSystem game object in your scene. In the Inspector, find the EventSystem component and populate the "First Selected" field with the UI game object that should receive initial focus. You may need to check the "Force input module" flag in the "Standalone Input Module" component. 

This allows you to navigate your UI via the keyboard while running in the Editor and via Apple TV Remote swipes and full stop click when running on your device.

**Note**: Apple TV Remote navigation does not work while running in the TV Simulator.

## Adding leaderboard resources to Xcode project
Game Center requires custom visual resources to be provided for its native leaderboard UI. Here are quick instructions on how to set them up in Xcode:

* Select Images.xcassets in Xcode project
* Right-click under listed files, and from the menu pick **Game Center &gt; New AppleTV Leaderboard**.
* Add your images.
* Select Leaderboard and on the right pane pick Edit View. Find the "Identifier" field and enter your leaderboard ID there.
* If after these modifications your asset compilation starts to fail, try disabling "On Demand Resources" in Xcode "Build Settings".

<a name="OnDemandResources"></a>
##Implementing On Demand Resources support

tvOS has strict requirements on how much disk space your application can reserve. The main application installation bundle size can not exceed 200 MB. However, the limits for additional downloadable content are much higher (up to 2GB for in-use assets and up to 20GB of total downloadable content). Apple recommends On Demand Resources (ODR) for tvOS downloadable content, as it enables the best disk space management strategies for tvOS. Unity supports ODR via Asset Bundles. An ODR implementation guide can be found in our dedicated  [blogpost](http://blogs.unity3d.com/2015/11/26/mastering-on-demand-resources-for-apple-platforms/) on the subject.

## Known limitations
* On-screen keyboard is limited to single line entries.
* tvOS Simulator does not emulate the Apple TV Remote as a Game Controller, thus making its input inaccessible to games.