# Facebook Player Settings

This page details the __Player Settings__ specific to the Facebook platform. A description of the general Player Settings can be found [here](class-PlayerSettings).

Note that the Facebook build target is utilizing the existing [WebGL](class-PlayerSettingsWebGL) and Windows [Standalone](class-PlayerSettingsStandalone) build targets, so the Player Settings for those targets will also apply.

## Publishing settings

![](../uploads/Main/class-PlayerSettingsFacebook-0.png)

| Property| Function |
|:---|:---| 
| Facebook SDK Version| Select the Facebook SDK Version for your project to use. This menu will be populated with new versions compatible with your version of Unity as Facebook publishes them. |
| AppID| Your Facebook AppID, used by Facebook to identify your app. See Facebook’s getting started page on how to set one up. |
| Upload access token| An upload access token, required to authorize the Unity editor to upload builds of your app to Facebook. You can get this from Facebook, on your app configuration page, under the "Web Hosting" tab. |
| Show Windows Player Settings| Open the Standalone Player settings, which affect any Facebook builds for Gameroom. |
| Show WebGL Player Settings| Open the WebGL Player settings, which affect any Facebook builds for WebGL. |
| FB.Init() Parameters| Some parameters affecting how the Facebook SDK is initialized on the facebook.com web page. Documented here. |

<br/>

---

* <span class="page-edit"> 2017-05-16  <!-- include IncludeTextNewPageNoEdit --></span>


