# Managing Remote Settings in the Unity Editor

The Remote Settings window helps you manage your remote settings while you are developing your project in the Editor. (Use the Unity Analytics Dashboard to [create and edit the settings](UnityAnalyticsRemoteSettingsCreating) themselves.)

The Remote Settings window is not included in the standard Unity download and install. It is part of the Remote Settings Asset package, which is a Unity plug-in. Download the Remote Settings Asset package from the [Unity Asset Store](https://www.assetstore.unity3d.com/#!/content/89317) and import it into your project.

To open the Remote Settings window, go to __Window__ > __Unity Analytics__ > __Remote Settings__ in the Unity Editor. In order for the Editor to fetch your Remote Settings from the Analytics Service, you must first supply the Project Secret Key as described in [Enabling Remote Settings](UnityAnalyticsRemoteSettingsEnabling).

The Remote Settings window, part of the [Remote Settings plug-in](https://www.assetstore.unity3d.com/#!/content/89317), displays the key-value pairs for the settings defined on your Analytics Dashboard.

![Remote Settings window](../uploads/Main/AnalyticsRemoteSettingsWindowValues.png)

Click __Refresh__ to fetch the latest remote settings. The Editor also fetches the most recently synchronized settings when you enter Play mode. 

Set __Active Configuration__ to __Release__ or __Development__ to choose which set of key-value pairs to work with in the Editor. Note that the __Development__ configuration is always used in Play mode in the Editor. To test the __Release__ configuration, use __File__ > __Build and Run__, and make sure that the __Development Build__ box is unchecked on the [Build Settings window](BuildSettings). 

---

* <span class="page-edit">2017-05-30 <!-- include IncludeTextNewPageYesEdit --></span>

* <span class="page-edit">2017-05-30 - Service compatible with Unity 5.5 onwards at this date but version compatibility may be subject to change.</span>
 
* <span class="page-history">New feature in 2017.1</span> 
