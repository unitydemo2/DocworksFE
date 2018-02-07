# Gradle for Android

Gradle is an Android build system which automates a number of build processes. This automation means that many common build errors are less likely to occur. Most notably in Unity, it reduces the method reference count in DEX (Dalvik Executable format) files, meaning that you are less likely to come across DEX limit problems. However, due to the differences between Gradle and the default Unity Android build system, some existing projects may be hard to convert to Gradle.

You can either build the output package (APK) using the Gradle build system in Unity, or export the Gradle project and build it in an external tool (such as Android Studio).

To learn more, see Gradle’s resources on [Getting Started with Gradle for Android Build](https://gradle.org/getting-started-android-build/).

## Building with Gradle for Android

To build your Android build with Gradle in Unity: 

1. In the Unity Editor, open the  [Build Settings](BuildSettings) window (menu: __File__ &gt; __Build Settings...__) 
2. In the __Platform__ list, select __Android__ 
3. Set the Build System drop-down to __Gradle (new)__, then click __Build__

![Gradle build settings](../uploads/Main/gradlebuildsettings.png)

## Exporting the Gradle project

To export a Gradle project, follow the instructions above, but tick the __Export Project__ option in the Build window before you click __Build__. When you click __Build__ Unity generates a Gradle project in the specified directory rather than building the APK. Import this project into Android Studio to make additional modifications or to get full control of the build process.

See [Android Studio's documentation on configuring your build](https://developer.android.com/studio/build/index.html) for more information about building an output package (APK).

## Providing a custom build.gradle template

To use your own build.gradle file when building the APK from Unity, use the Custom Gradle Template checkbox under [Player Settings](class-PlayerSettingsAndroid). 
This will generate a default mainTemplate.gradle for you, which you can edit. This template contains several variables that will be filled in by the Unity build process, such as `**TARGETSDKVERSION**` – you would normally leave these alone.
You can also use your own settings.gradle by providing a settingsTemplate.gradle in your Plugins directory in the same way (although there is currently no automatic way to do this). This file is responsible for including your library projects, so unless you want to also override that process, the file should at least contain this line: 

`**INCLUDES**`

which will be replaced by include directives to all your libraries.

###Template Variables
These variables can be used in the mainTemplate.gradle file;

|**Variable:** |**Description:** |
|:---|:---|
|__DEPS__| List of project dependencies; ie the libraries used. |
|__API VERSION__ | API version to build for (eg 25). |
|__BUILDTOOLS__| SDK Build tools used (eg 25.0.1). |
|__TARGETSDKVERSION__ | API version to taget (eg 25). |
|__APPLICATIONID__ | Android Application ID (eg com.mycompany.mygame). |
|__MINIFY_DEBUG__| Minify for debug builds enabled (true or false). |
|__PROGUARD_DEBUG__ | Use proguard for minification (true or false.) |
|__MINIFY_RELEASE__ | Minify for release builds enabled (true or false). |
|__PROGUARD_RELEASE__| Use proguard for minification (true or false). |
|__USER_PROGUARD__ | Custom user proguard file (ie progard-user.txt). |
|__SIGN__ | Complete signingConfigs section if build is to be signed. |
|__SIGN_CONFIG__ | Set to ‘signingConfig signingConfig.release’ if build is signed. |
|__DIR_GRADLEPROJECT__ | Directory where the gradle project is created. |
|__DIR_UNITYPROJECT__ | Directory of your Unity project. |

###Minification
You can activate **Proguard Minification** under [Player Settings](class-PlayerSettingsAndroid) Minify. 
Note that proguard can easily strip out code that is actually needed, so often this process needs to be configured carefully. You can generate a custom proguard.txt using the checkbox User Proguard File under the same settings as a starting point. 

See the [ProGuard manual](https://www.guardsquare.com/en/proguard/manual/usage) for more information on Proguard.


## Errors when building with Gradle

If an error occurs during building for Android using Gradle, Unity displays an error dialog box. Click __Troubleshoot__ to open the [Gradle troubleshooting](android-gradle-troubleshooting) Unity documentation in your system’s browser.

![Unity’s Grade build error dialog box](../uploads/Main/gradleerrorapk.png)

---

* <span class="page-edit"> 2017-10-02  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Expanded custom build.gradle template section.</span>

* <span class="page-history">New feature in 5.5</span>
