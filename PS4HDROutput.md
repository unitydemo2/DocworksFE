# PS4 HDR output

This page explains how to enable HDR output on any PS4 console (PS4 Pro and base PS4).

Configuring HDR output only configures the PS4 and TV to transfer HDR format frame data between each other. It does not generate the correct HDR color space graphic data. You need to handle that in your code. For more information, see the [Initial HDR Guide for SDK 4.00](https://ps4.siedev.net/projects/sdk/dl/dl/1930/10099/Initial%20HDR%20Guide%20for%20SDK%204.00.pdf).

You need to ensure that your game code generates appropriate [BT2020 HDR](https://en.wikipedia.org/wiki/Rec._2020) frame data for the final output buffer. This requires game-specific shaders that should be part of the post processing chain. Without these shaders, the output appears in the wrong color space, and at the wrong brightness level. If your game contains any 2D UI elements, you might need to incorporate special handling for those elements. 

For more information, see the [PlayStation®4 HDR Support Overview](https://ps4.siedev.net/projects/sdk/dl/dl/1930/10098/PS4%20HDR%20Support%20Overview%20v1.0%20en.pdf).

## Configuring an HDR title

To use HDR in your game, set the game to run in HDR mode. To do this, go to __File__ > __Build Settings__ > __Player Settings__ > __Other Settings__ > __Use display in HDR mode__. This sets the HDR attribute in the .sfo application file, and causes a warning dialog box at startup in order to comply with the PS4 technical requirement checklist (TRC).

The application starts outputting an HDR signal to the TV. You can then set the initial color depth to HDR; go to __File__ > __Build Settings__ > __Resolution and Presentation__ and set __Color Depth__ to __HDR__.


## Handling HDR in-game

When you have configured HDR, the game launches with output mode set to HDR. You need to:

1. Check the current video output mode on your PS4.
2. Detect whether your PS4 and TV setup supports HDR.
3. Change to SDR video output mode if HDR isn’t supported.
4. Use the correct set of assets/shaders according to video output mode.

**Note**: You should insert the code snippets in the following steps into your initialisation code (for example, inside an `Awake()` function for a GameObject in the first Scene).

### 1. Check the current video output mode on your PS4

Use the following code to detect whether the PS4 is currently configured for HDR output:

```
UnityEngine.PS4.Utility.VideoOutMode requestedVideoOutMode;
UnityEngine.PS4.Utility.GetRequestedVideoOutMode(out requestedVideoOutMode);
if ((requestedVideoOutMode.colorimetry == UnityEngine.PS4.Utility.VideoOutColorimetry.BT2020_PQ)||
            (requestedVideoOutMode.colorimetry == UnityEngine.PS4.Utility.VideoOutColorimetry.RGB2020_PQ) ||
            (requestedVideoOutMode.colorimetry == UnityEngine.PS4.Utility.VideoOutColorimetry.YCBCR2020_PQ))
	Debug.Log("Currently outputting HDR data");
```

The following table shows the expected results from calling `GetRequestedVideoOutMode` depending on whether __Use display in HDR mode__ is set to on or off, with different hardware HDR settings:


|**Unity setting**|**Device setting**|**Results**||
|__Display in HDR mode__ |**TV/PS4 HDR**|**GetRequestedVideoOutMode**|
|:---|:---|
|On| On - Both |BT2020_PQ|
|Off|On - Both|Any|
|On|Off - Either|BT2020_PQ|
|Off|Off - Either|Any|

### 2. Detect whether your PS4 and TV setup supports HDR


Use the following code to detect whether the PS4 and TV setup can support HDR:

```
UnityEngine.PS4.Utility.VideoOutDeviceCapability videoDeviceCap = UnityEngine.PS4.Utility.GetVideoOutDeviceCapability(UnityEngine.PS4.Utility.videoOutPortHandle);
if ((videoDeviceCap & UnityEngine.PS4.Utility.VideoOutDeviceCapability.BT2020_PQ) != 0)
	Debug.Log("Setup Supports HDR");
```

The following table shows the expected results from calling `GetVideoOutDeviceCapability` depending on whether __Use display in HDR mode__ is set to on or off, with different hardware HDR settings:

|**Unity setting**|**Device setting**|**Results**||
|__Display in HDR mode__ |**TV/PS4 HDR**|**GetVideoOutDeviceCapability**|
|:---|:---|
|On| On - Both |YUV, XVYCC, BT2020_PQ|
|Off|On - Both|YUV, XVYCC|
|On|Off - Either|YUV, XVYCC|
|Off|Off - Either|YUV, XVYCC|

**Note**: If __Use display in HDR mode__ is unchecked in the Unity Editor, this will always return without HDR Support.

You can configure PS4 dev kits to always return that they are connected to an HDR TV by selecting __Debug Settings__ > __Sound and Screen__ > __Force HDR Capability__.


### 3. Change between HDR and SDR video output modes

Use this script code to request a change from SDR output to HDR:

```
UnityEngine.PS4.Utility.videoOutPixelFormat = UnityEngine.PS4.Utility.VideoOutPixelFormat.HDR;
```

**Note**: Before changing to HDR, always check your device has HDR support. Your application hangs if you change to HDR on a device which does not have HDR support. See PS4 documentation on [TRC item 4089](https://ps4.scedev.net/resources/documents/TRC/2017.10/TRC/R4089.html) for more details.

To request a change from HDR output to SDR, use this script code:

```
UnityEngine.PS4.Utility.videoOutPixelFormat = UnityEngine.PS4.Utility.VideoOutPixelFormat.Regular;
```

When HDR isn’t possible, you can use these scripts to change to SDR properly: [TRC item R4202](https://ps4.scedev.net/resources/documents/TRC/2017.10/TRC/R4202.html).

### 4. Use the correct set of assets/shaders according to video output mode

When you have set the right output mode, you need to load and use the appropriate set of assets for HDR or SDR display. You can do this using AssetBundle Variants, as shown in the [AssetBundles and AssetBundle Manager tutorial](https://unity3d.com/learn/tutorials/topics/scripting/assetbundles-and-assetbundle-manager).


---

* <span class="page-edit">2017-10-17  <!-- include IncludeTextNewPageYesEdit --></span>

* <span class="page-history">PS4 HDR support added in Unity 5.6</span>






