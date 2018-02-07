# Troubleshooting Android development

While developing for Android using Unity, you could encounter a number of issues. Problems are often related to plug-ins or incorrect Project settings. This section outlines the most common scenarios and relavant troubleshooting advice. 

## Your application crashes immediately after launch

1. Remove any native plug-ins you have.

2. Disable stripping.

3. Use `adb logcat` to get the crash report from your device. Consult the official [Android Developer Logcat Command-Line Tool documentation](https://developer.android.com/studio/command-line/logcat.html) for more information.

## The game crashes after a couple of seconds when playing video

Ensure __Settings__ > __Developer Options__ > __Don’t keep activities__ isn’t enabled on the device.

The video player is its own activity, and therefore regular game activity will be destroyed if the video player is activated.

## No Android device found

If Unity cannot find an Android device connected to the system, check the following:

1. Make sure that your device is actually connected to your computer - check the USB cable and the sockets.

2. Make sure that your device has __USB Debugging__ enabled in the Developer options. For more details, refer to the [Android SDK/NDK Setup](android-sdksetup) page.

3. Run the `adb devices` command from the `platform-tools` directory of your Android SDK installation and check the output.

    * If the output list is empty and you are using Windows, you may need to install the driver for ADB devices. For more details, refer to the [Android SDK/NDK Setup](android-sdksetup) documentation.

    * If the list contains entries with the __unauthorized__ label, you may need to authorize your computer on your device and give it permission to debug it. Check the device’s screen for the corresponding dialog.

    * If the list contains your device with the __device__ label, build your Project in Unity again.

## Failed to re-package resources

This error occurs when the Android Asset Packaging Tool (AAPT) fails. AAPT is used to build the intermediate Asset packages during Android build. This issue is most often caused by missing resources or duplicate resources in your Android plug-ins.

Check the console message for more details - it should contain the IDs of the resources that are missing or duplicates. Fix the error in your plug-ins by either adding the missing resources/settings or removing the duplicate plug-ins.

## Unable to merge Android manifests

The most likely cause for this issue is that one of your plug-ins has a manifest that is incompatible with the main Unity manifest.

Check the console message for more details on which attributes are conflicting, and fix the manifests accordingly. 

See the [Android Manifest](android-manifest) documentation for more details on Android manifests.

## Unable to convert classes into DEX format

The most likely cause for this issue is that you have a Java plug-in added twice. This results in duplicate classes when Unity tries to build a DEX (Dalvik Executable Format) file from all the compiled Java plug-ins. Check the console output for the list of duplicate entries, and fix the plug-ins.

If your console messages says "Too many references", it means that the number of fields and methods exceeded the DEX limit of 64k. This usually happens when the number of plug-ins or plug-in resources is too high. Due to the way the references are generated, the limit could be hit with just a couple of large plug-ins.

There are several ways to handle this issue. One of these is by stripping the plug-ins. However, the quickest way to fix it is to switch to the [Gradle build system](android-gradle-overview), or export the Project and build it in [Android Studio](https://developer.android.com/studio/index.html).

## Unable to install APK to device

This error can be caused by:

* Installing to an incompatible device.

* Installing to a device running a version of Android lower than the __Minimum API Level__ in your Player settings. 

Check the console for the actual error code and output. 

----
* <span class="page-edit">2017-05-25 <!-- include IncludeTextNewPageYesEdit --></span>

* <span class="page-history">Updated functionality in 5.5</span>