# Reporting crash bugs under Android

Before submitting a bug report, refer to the [Troubleshooting Android development](TroubleShootingAndroid) page of the Unity Manual and the [Unity Android forum](https://forum.unity3d.com/forums/android.30/) for solutions to common crashes and problems. 

Investigating crashes on Android can be challenging, especially if you cannot reproduce the crash on your own device. use the [Android Debug Bridge (ADB)](https://developer.android.com/studio/command-line/adb.html) to create a log from your device by running `adb logcat`. Information about what the ADB logcat file contains can be found on the [logcat command line tool](https://developer.android.com/studio/command-line/logcat.html) page of the official Android Studio documentation.

If you are unable to find a solution to your problem through the above methods, submit a bug report and attach the ADB logcat file and the full Unity Project to your bug report before submitting, following the [Unity bug reporting guidelines](https://unity3d.com/unity/qa/bug-reporting.).