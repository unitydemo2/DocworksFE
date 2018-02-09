# Unity Remote

Unity Remote is a downloadable app designed to help with Android, iOS and tvOS development. The app connects with Unity while you are running your project in Play Mode from the editor. The visual output from the editor is sent to the device's screen, and the live inputs are sent back to the running project in Unity. This allows you to get a good impression of how your game really looks and handles on the target device, without the hassle of a full build for each test.

Unity Remote replaces the separate iOS and Android Remote apps used with earlier versions. Those older Remote apps are no longer supported.

*Older versions of Unity Remote are still available for use in Legacy projects; see [Legacy Unity Remote](LegacyUnityRemote) documentation for more information on these versions.*


##Device and Feature Support

Unity Remote currently supports Android devices (on Windows and OS X via a USB connection) and iOS devices (iPhone, iPad, iPod touch and Apple TV, through USB on OS X and Windows with iTunes).

The Game View of the running Unity project is duplicated on the device screen, but at a reduced framerate. The following input data from the device is also streamed back to the editor:

* Touch and stylus input
* Accelerometer
* Gyroscope
* Device camera streams
* Compass
* GPS
* Joystick names and input

Note that the Remote app simply shows the visual output on the device and takes input from it. The game's actual processing is still done by the Unity editor on the desktop machine - so its performance is not a perfect reflection of the built app.

## Obtaining and Using Unity Remote

Unity Remote can be downloaded for free in the form of a Unity project that you build yourself, or as a pre-built app from the device's app store:

* **Unity Project** (requires custom building) from the [Asset Store](https://www.assetstore.unity3d.com/#/publisher/1)
* **Android app** from [Google Play](https://play.google.com/store/apps/details?id=com.unity3d.genericremote)
* **iOS and tvOS apps** from the [App Store](https://itunes.apple.com/us/app/unity-remote-4/id871767552)


Once you've downloaded the app, install and run it on your device and connect the device to your computer using a USB cable.

To enable Unity to work with your device, open the Editor Settings in Unity (menu: __Edit &gt; Project Settings &gt; Editor__) and select the device to use from the __Unity Remote__ section:

![](../uploads/Main/UniRemoteEdSettings5.png)

Click the Play button in the editor to see your game appear on the device and in the Unity game window as Unity connects to the Remote app. While the game plays, input from the device (accelerometer, etc) is sent to your scripts as if they were running on the device itself.

##Troubleshooting

###I have more than one device plugged in, but only one of them works with Unity

Unity Remote doesn't support multiple connected Android devices, and to resolve this, it will automatically pick the first device it finds. However, it is fine to have multiple iOS/tvOS devices and one Android device connected at the same time, since you can select which one to use from the Editor Settings (menu: __Edit &gt; Project Settings &gt; Editor__).

###I'm getting really poor graphics quality when running my game in Unity Remote

When you use Unity Remote the game actually runs in the Unity editor, while its visual content is streamed to the target device. Since the bandwidth between editor and device is limited, the stream must be compressed heavily for transmission. This compression inevitably reduces the image quality.

In the __Unity Remote__ section of the Editor settings (menu: __Edit &gt; Project Settings &gt; Editor__) you can switch the compression method between JPEG and PNG, and also optionally downsize the resolution of the screen image. PNG compression is "lossless" (so the image quality doesn't degrade) but uses more bandwidth than JPEG. A downsized image has lower bandwidth requirements than one at full resolution. By changing these settings, you can trade image accuracy off against framerate as necessary.

Bear in mind that Unity Remote is only really intended to give a quick approximate check of how your game will look and feel when running on the device. Make sure that you occasionally do a full build and test the "real" app.

