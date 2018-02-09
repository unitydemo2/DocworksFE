# Android Manifest

The Android Manifest is an XML file which contains important metadata about the Android app. This includes the package name, activity names, main activity (the entry point to the app), configurations, Android version support, hardware features support, and permissions.

For more information about the Android Manifest file, refer to the Android Developer documentation on [Android Manifests](https://developer.android.com/guide/topics/manifest/manifest-intro.html).

## How Unity produces the Android Manifest

When building your app, Unity automatically generates the Android Manifest, following the steps below:

1. Unity takes the main Android Manifest.

2. Unity finds all the Android Manifests of your plug-ins (AARs and Android Libraries).

3. Manifests from plug-ins are merged into the main Manifest using Google’s [manifmerger](https://android.googlesource.com/platform/sdk/+/0386f5d/manifmerger) class.

4. Unity modifies the Manifest, automatically adding permissions, configuration options, features used, and other information to the Manifest.

## Overriding the Android Manifest

Although Unity generates a correct Manifest for you, in some cases you might want direct control over its contents.

To use an Android Manifest that you have created outside of Unity, import your Android Manifest file to the following location: _Assets/Plugins/Android/AndroidManifest.xml_. This overrides the default Unity-created Manifest.

In this situation, Android Libraries’ Manifests are later merged into your main Manifest, and the resulting Manifest is still tweaked by Unity to make sure the configuration is correct. For full control of the Manifest, including permissions, you need to export the Project and modify the final Manifest in [Android Studio](https://developer.android.com/studio/index.html?gclid=CPbCm_HwptICFVXnGwodghYK5w).

## Permissions

Unity automatically adds the necessary permissions to the Manifest based on the [Player Settings](class-PlayerSettingsAndroid) and Unity APIs that your app calls from the script. For example:

* [Network](ScriptRef:Network.html) classes add the `INTERNET` permission

* Using vibration (such as [Handheld.Vibrate](ScriptRef:Handheld.Vibrate.html)) adds `VIBRATE`

* The [InternetReachability](ScriptRef:Application-internetReachability.html) property adds `ACCESS_NETWORK_STATE`

* Location APIs (such as [LocationService](ScriptRef:LocationService.html)) adds `ACCESS_FINE_LOCATION`

* [WebCamTexture](ScriptRef:WebCamTexture.html) APIs add `CAMERA` permission

* The [Microphone](ScriptRef:Microphone.html) class adds `RECORD_AUDIO`

For more information about permissions, see the [Android Manifest Permissions](https://developer.android.com/guide/topics/manifest/manifest-intro.html#perms) page of the Android Developer documentation.

Note that if your plug-ins require a permission by declaring it in their Manifests, the permission is automatically be added to the resulting Android Manifest during the merge stage. Any Unity APIs called by the plug-ins also contribute to the permission list.

## Runtime permissions in Android 6.0 (Marshmallow)

If your app is running on a device with Android 6.0 (Marshmallow) or later and also targets Android API level 23 or higher, your app uses the Android [Runtime Permission System](https://developer.android.com/training/permissions/requesting.html).

The Android Runtime Permission System asks the app’s user to grant permissions while the app is running, instead of when the app is first installed.  App users can usually grant or deny each permission when the app needs them while the app is running (for example, requesting camera permission before taking a picture). This allows an app to run with limited functionality without permissions. 

Unity does not support the Runtime Permission System, so your app prompts the user to allow what Android calls "dangerous" permissions on startup. See Android's  documentation on [dangerous permissions](https://developer.android.com/guide/topics/permissions/requesting.html) for more information.

Prompting your user to allow dangerous permissions is the only way to ensure plug-ins don’t cause crashes when they are missing a permission.  However, if you don’t want your Unity Android app to ask for permissions on startup, you can add the following to your Manifest in either the __Application__ or __Activity__ sections.

```
<meta-data android:name="unityplayer.SkipPermissionsDialog" android:value="true" />

```

Adding this completely suppresses the permission dialog shown on startup, but you must handle runtime permissions carefully to avoid crashes. This method is only recommended for advanced Android app developers.

For further information about the Runtime Permission System and handling permissions, see the [Requesting Permissions](https://developer.android.com/training/permissions/requesting.html) section of the Android Developer documentation. 

## Examining the resulting Android Manifest

To examine the final Android Manifest that Unity has generated for your app, open the _Temp/StagingArea/AndroidManifest.xml_ file after you have built your Project but before exiting the Unity Editor.

The Manifest is stored in binary format in the output package (APK). To check the contents of a Manifest inside an APK, you can use the [Android Studio APK Analyzer](https://developer.android.com/studio/build/apk-analyzer.html) or another third-party tool (such as [Apktool](https://ibotpeaches.github.io/Apktool/)).