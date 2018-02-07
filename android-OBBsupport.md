# Support for APK expansion files (OBB)

APK expansion files are used as a solution for the 100MB app size limit in the Google Play Store. If your app is larger than 100MB (which is quite likely for a big game), you have to split your output package into the main part (APK) and the expansion file (OBB). Refer to the Android Developer documentation on [expansion files](https://developer.android.com/google/play/expansion-files.html) for more information.

Unity automatically splits the output package into APK and OBB. This is not the only way to split the app package (other options include third-party plug-ins and [AssetBundles](https://docs.unity3d.com/Manual/AssetBundlesIntro.html)), but it is the only automatic splitting mechanism officially supported by Unity.

## Building the app with expansion files

If you want Unity to split the app output package into APK and OBB for you, open the __Player Settings__ window (menu: __Edit__ > __Project Settings__ > __Player__), and in the __Publishing Settings__ section, tick the __Split Application Binary__ checkbox.

![The __Publishing Settings__ section of the __Player Settings__ window, with the __Split Application Binary__ checkbox highlighted](../uploads/Main/android-OBB-0.png)

Both parts of the output package (APK and OBB) are copied to the output directory you specify when building the app. For example, if the APK has the name _mygame.apk_, the OBB is in the same directory under the name _mygame.main.obb_.

If you select __Build and Run__, the APK and OBB files are installed on your device by Unity. If you select __Build __and want to install the app manually using the ADB utility, you must first install the APK and then copy the OBB into the correct location on your device. The OBB file name must correspond the format required by Google. Refer to the [expansion files](https://developer.android.com/google/play/expansion-files.html) section of the Android Developer documentation for more information. 

If the app starts and can’t find and load the OBB, only the first Scene is available (see documentation on how data is split between the APK and OBB below for more information). Do not use the contents of the OBB separately - always treat the APK and OBB as a unique bundle, the same way as you would treat a single APK.

## How data is split between the APK and OBB

When the __Split Application Binary__ option is enabled, the app is split the following way:

* __APK__ - Consists of the executables (Java and native), plug-ins, scripts, and the data for the first Scene (with the index 0).

* __OBB__ - Contains everything else, including all of the remaining Scenes, resources, and streaming Assets.

If your APK is still too large for publishing in the Google Play Store (more than 100MB), try reducing the size of your first Scene, making it as small as possible.

## Downloading the OBB expansion file

[The Unity Asset Store offers a plug-in](https://www.assetstore.unity3d.com/en/#!/content/3189) that allows you to access an adapted version of the Google Play `market_downloader` library for Unity, which you can use to download the OBB from Google Play Store, or an external source, and move it into the correct directory.

## Hosting OBB files on the Google Play Store

OBB expansion files should be published to the Google Play Store along with your APK. Any OBB files published with your APK will be automatically downloaded when a user installs your app from the Google Play Store. 

You should include code in your app that downloads missing OBB files in the case of a Google Play Store error, or if a user removes the OBB files from their device. For more information about downloading OBB files, refer to the [APK Expansion file](https://developer.android.com/google/play/expansion-files.html#DownloadProcess) section of the Android Developer documentation.

## Hosting OBB files without using the Google Play Store

You can also host OBB files yourself if you do not want to use the Google Play Store. However, hosting OBB files without using the Google Play Store  is only recommended
for advanced users.

----
* <span class="page-edit">2017-05-25 <!-- include IncludeTextNewPageYesEdit --></span>

* <span class="page-history">Updated functionality in 5.5</span>
