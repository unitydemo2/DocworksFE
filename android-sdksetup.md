# Android SDK/NDK setup

Whether you’re building an Android application in Unity or programming it from scratch, you need to set up the Android Software Development Kit (SDK) before you can build and run any code on your Android device.

### 1. Download the Android SDK

Download the Android SDK from the [Android Studio and SDK Tools download page](https://developer.android.com/studio/index.html). You can either use an Android Studio and SDK bundle, or only download the SDK command line tools.

### 2. Install the Android SDK

Install or unpack the Android SDK. After installing, open the Android SDK Manager and add at least one Android SDK Platform, the Platform Tools, the Build Tools, and the USB drivers if you’re using Windows.

### 3. Enable USB debugging on your device

To enable USB debugging, you need to enable Developer options. To do this, find the build number in your device’s __Settings__ menu. The location of the build number varies between devices. The stock Android setting can be found by navigating to __Settings__ > __About phone__ > __Build number__. For different devices and Android versions, refer to your hardware manufacturer. 

![Build number as displayed in Android 5.0 (Lollipop) on a Samsung Galaxy Note 3](../uploads/Main/android-sdksetup-0.png)

__Note:__ On operating systems older than Android 4.2 (Jelly Bean), the Developer options aren’t hidden. Go to __Settings__ > __Developer options__, then enable USB debugging.

After you have navigated to the build number using the instructions above, tap on the build number seven times. A pop-up notification saying "You are now X steps away from being a developer" appears, with "X" being a number that counts down with every additional tap. On the seventh tap, Developer options are unlocked. Go to __Settings__ > __Developer options__, and check the USB debugging checkbox to enable debug mode when the device is connected to a computer via USB.

![Developer options as displayed in Android 5.0 (Lollipop) - Samsung Galaxy Note 3](../uploads/Main/android-sdksetup-1.png)

### 4. Connect your Android device to the SDK

Connect your Android device to your computer using a USB cable. If you are developing on a Windows computer, you need to install the appropriate USB driver for your device. 

For more information on connecting your Android device to the SDK, refer to the [Running Your App](https://developer.android.com/training/basics/firstapp/running-app.html#Emulator) section of the Android Developer documentation.

### 5. Configure the Android SDK path in Unity

The first time you make a Project for Android (or if Unity later fails to locate the SDK), you will be asked to locate the folder where you installed the Android SDK. Select the root folder of your SDK installation. If you wish to change the location of the Android SDK, in the menu bar go to __Unity__ > __Preferences__ > __External Tools__.

### 6. Download and set up the Android NDK

If you are using the [IL2CPP](IL2CPP) scripting back end for Android, you need the Android Native Development Kit (NDK). It contains the toolchains (such as compiler and linker) needed to build the necessary libraries, and finally produce the output package (APK). If you are not targeting the IL2CPP back end, you can skip this step.

Download the Android NDK version required by Unity from the [NDK Downloads](https://developer.android.com/ndk/downloads/index.html) web page, and then extract it to a directory. The first time you build a project for Android using IL2CPP, you will be asked to locate the folder where you installed the Android NDK. Select the root folder of your NDK installation. If you wish to change the location of the Android NDK, in the Unity Editor, navigate to menu: __Unity__ > __Preferences...__ to display the Unity Preferences dialog box. Here, click  __External Tools__.

----

* <span class="page-edit">2017-05-25 <!-- include IncludeTextNewPageYesEdit --></span>

* <span class="page-history">Updated functionality in 5.5</span>