# Getting started with Android development

Building games for Android devices requires an approach similar to that for iOS development. However, the hardware is not completely standardized across all devices, and this raises issues that don’t normally appear during development for iOS.

## Setting up your Android development environment

You need to have your Android development environment set up before testing your Unity applications on your Android device. Setting up your Android development environment involves the following steps:

1. Download and install the [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

2. Download and install the [Android Software Development Kit (SDK)](https://developer.android.com/studio/index.html) with the relevant Android platforms, platform tools and build tools for your Project.

3. Connect your device to your computer. The setup process differs for Windows and macOS, and is explained in detail on the [Android developer website](http://developer.android.com). Refer to your device manufacturer for specific information about connecting it to your computer.

4. Download and install the [Android Native Development Kit (NDK)](https://developer.android.com/ndk/index.html) if you are using the IL2CPP scripting back end.

The Unity Manual contains a [basic outline](https://docs.unity3d.com/Manual/android-sdksetup.html) of the tasks that must be completed before you are able to run code on your Android device, or in the Android emulator. However, the best thing to do is follow the instructions step-by-step from the [Android developer portal](http://developer.android.com/sdk).

Unity verifies your development environment when building for Android, and prompts you to upgrade or download missing components if necessary. Always use the latest tools available unless a specific version is required by Unity.

## Access Android functionality

Unity provides scripting APIs to access various input data and settings from Android devices.

Refer to the [Android scripting page](android-API) of the Manual for more information.

## Exposing native C, C++ or Java code to scripts

Use plug-ins to call Android functions written in C/C++ directly from C# scripts (Java functions can be called indirectly).

To find out how to make these functions accessible from within Unity, visit the [Android plug-ins page](PluginsForAndroid).

## Occlusion culling

Unity includes support for occlusion culling, which is a valuable optimization method for mobile platforms.

Refer to the [Occlusion Culling](OcclusionCulling) Manual page for more information.

## Splash screen customization

The splash screen displayed while the game launches is customizable on Android.

Refer to the [Customizing an Android Splash Screen](AndroidMobileCustomizeSplashScreen) Manual page for more information. 

## Troubleshooting and bug reports

The [Android troubleshooting guide](TroubleShootingAndroid) helps you discover the cause of bugs as quickly as possible. If, after consulting the guide, you suspect the problem is being caused by Unity, file a bug report following the Unity bug reporting guidelines.

See the [Android bug reporting page](android-bugreporting) for details about filing bug reports.

## Texture compression

ETC is the standard texture compression format on Android.

ETC1 is supported on all current Android devices, but it does not support textures that have an alpha channel. ETC2 is supported on all Android devices that support OpenGL ES 3.0. It provides improved quality for RGB textures, and also supports textures with an alpha channel.

By default, Unity uses ETC1 for compressed RGB textures and ETC2 for compressed RGBA textures. If ETC2 is not supported by an Android device, the texture is decompressed at run time. This has an impact on memory usage, and also affects rendering speed.

DXT, PVRTC, ATC, and ASTC are all support textures with an alpha channel. These formats also support higher compression rates and/or better image quality, but they are only supported on a subset of Android devices.

It is possible to create separate Android distribution archives (.apk) for each of these formats and let the Android Market’s filtering system select the correct archives for different devices.

## Movie playback

Movie textures are not supported on Android, but full-screen streaming playback is provided via scripting functions.

To learn about supported file formats and scripting API, consult the [Movie Texture page](MovieTexture) or the [Android supported media formats page](media-formats).

