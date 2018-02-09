# Getting started with Facebook development

## What is the Facebook build target?

The Facebook build target makes it easy to publish Unity games to Facebook and to use Facebook functionality in your games. Using the Facebook build target, you can build your content either as a [WebGL](#webgl-gettingstarted) player, which you can then publish to [facebook.com](http://facebook.com), or as a custom native [Windows Standalone](#class-PlayerSettingsStandalone) player, which you can the publish to the [Facebook Gameroom](https://www.facebook.com/gameroom/) client.

When the Facebook build target is selected, you automatically have access to the [ Facebook SDK](https://developers.facebook.com/docs/unity/) in your scripts, which lets you interact with Facebook and access it’s social features.

## Publishing your game to Facebook

### Configuration

To publish your game to Facebook, you first need to[ create a new App on the Facebook developer page](https://developers.facebook.com/?advanced_app_create=true). Once completed, this will give you an AppID, which you should paste into your[ Facebook PlayerSettings](#class-PlayerSettingsFacebook). Now, you can get an *Upload access token* from Facebook, on your app configuration page, under the __Web Hosting__ tab. Also paste this into your Facebook Player Settings. This will allow you to upload your game to Facebook directly from the Unity Editor.

### Building

Access the Facebook Build Settings via the in the __Build Settings__ dialog box (menu: __File__ > __Build Settings…__). In the dialog box, select __Facebook__ from the __Platform__ list.

![](../uploads/Main/Facebook-GettingStarted-0.png)

Here you can choose to build your content as WebGL or as a Windows Standalone for Gameroom. If you plan to upload your game, choose __Package build for uploading__, which generates a compressed package, which can be uploaded to facebook.

After making a build, the __Upload last build to Facebook__ button becomes available. If you have correctly configured your AppID and Upload access token, you can click this button to upload your build to facebook. The __Enter Comment for upload__ field lets you specify an optional comment to identify your build.

Once you have uploaded a build to Facebook, it will appear on your your app configuration page on Facebook, under the __Web Hosting__ tab. Here you can choose to push your build to production or to stage partial rollouts to smaller percentages of your users.

## Using the Facebook SDK

When the Facebook build target is active, you can use the Facebook SDK in your scripts. This lets you share content on Facebook, track analytics events, use Facebook Payments and more. See [Facebook’s documentation](https://developers.facebook.com/docs/unity/reference/current) for more information on how to use the SDK.

Which version of the SDK to use can be selected in the [Facebook PlayerSettings](#class-PlayerSettingsFacebook), which will show all versions which Facebook has made available for your version of Unity.

### Using a custom Facebook SDK

If you want to use a different build of the Facebook SDK then the one included by Unity by default, you can do that, as long as it at least version 7.9.1 (so it supports the Facebook build target). Just[ download](https://developers.facebook.com/docs/unity/downloads/) a build of the SDK from Facebook, and drop it into your Assets Folder. Unity will detect this, and disable the built-in SDK. This will allow you to use the Facebook SDK outside of the Facebook build target, which you want to use Facebook features on other platforms facebook supports.



<br/>

---

* <span class="page-edit"> 2017-05-16  <!-- include IncludeTextNewPageNoEdit --></span>

