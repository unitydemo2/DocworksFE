# Gradle for Android

Gradle is an Android build system which automates a number of build processes. This automation means that many common build errors are less likely to occur. Most notably in Unity, it reduces the method reference count in the DEX (Dalvik Executable format) files, meaning that you are less likely to come across DEX limit problems. However, due to the differences between Gradle and the default Unity Android build system, some existing projects may be hard to convert to Gradle.

You can either build the output package (APK) using the Gradle build system in Unity, or export the Gradle project and build it in an external tool (such as Android Studio).

To learn more, see Gradle’s resources on [Getting Started with Gradle for Android Build](https://gradle.org/getting-started-android-build/).

## Building with Gradle for Android

To build your Android build with Gradle in Unity: 

1. In the Unity Editor, open the  [Build Settings](BuildSettings) window (menu: __File__ > __Build Settings...__) 
2. In the __Platform__ list, select __Android__ 
3. Set the Build System drop-down to __Gradle (new)__, then click __Build__

![Gradle build settings](../uploads/Main/gradlebuildsettings.png)

## Exporting the Gradle project

To export a Gradle project, follow the instructions above, but tick the __Export Project__ option in the Build window before you click __Build__. When you click __Build__ Unity generates a Gradle project in the specified directory rather than building the APK. Import this project into Android Studio to make additional modifications or to get full control of the build process.

See [Android Studio's documentation on configuring your build](https://developer.android.com/studio/build/index.html) for more information about building an output package (APK).

## Providing a custom build.gradle template

To use your own _build.gradle_ file when building the APK from Unity, import your _build.gradle_ file to _Assets/Plugins/Android/mainTemplate.gradle_. Note that the file may use some template variables like TARGETSDKVERSION. See the default _mainTemplate.gradle_ file in the Unity installation for an example file.

## Errors when building with Gradle

If an error occurs during building for Android using Gradle, Unity displays an error dialog box. Click __Troubleshoot__ to open the [Gradle troubleshooting](android-gradle-troubleshooting) Unity documentation in your system’s browser.

![Unity’s Grade build error dialog box](../uploads/Main/gradleerrorapk.png)

