Unity Analytics Re-integrate SDK to 5.1
=================================



**Note: 5.1 Projects that Integrated Analytics Before September 8, 2015**
Unity Analytics SDK will now support 4.x-5.1 versions. The previous 5.1 integration "PlayerSettings" copy-and-paste ProjectID method will still work, but we are discontinuing support for it. Refer to [Analytics Forum](http://forum.unity3d.com/threads/unity-analytics-sdk-extended-support-for-4-x-5-1-versions.352198/) for more information. 

The process is divided into three general steps:  

1. Removal of existing Unity Analytics Project ID 
2. Re-integration of Unity Analytics
3. Updating of Advanced Integration events

1. Remove Existing Unity Analytics Project ID
------------------------------------------
Open Unity Editor 5.1 and select your existing Analytics project. Locate your Cloud Project ID in Player Settings.
Choose Edit-&gt;Project Settings-&gt;Player, which opens the Player Settings.
Delete your Cloud Project ID

![](../uploads/Main/AnalyticsUpgradeStrippingProjectID.gif)


2. Integrating Unity Analytics SDK
-------------------------------
Follow [Unity Analytics 4.x-5.1 (SDK) instructions](UnityAnalyticsSDK)


3. Updating Advanced Integration events
------------------------------------
If you did any existing Advanced Integration previously, you will also need to update the namespace and the calls to use the updated 4.x-5.1 SDK syntax.

Follow [4.x-5.1 (SDK) Advanced Integration instructions to update.
](UnityAnalyticsAdvancedSDK)
