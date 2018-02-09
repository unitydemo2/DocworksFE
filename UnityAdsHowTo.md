# How to use Unity Ads

Once you have [set up your project for Unity Services](SettingUpProjectServices), you can enable the Unity Ads service.

##Step 1: Enable ads for your game in the Editor

1. Open the Ads configuration window from __Window__ > __Services__ > __Ads__  
![Open Drawer](../uploads/UnityAds/openDrawer.png)
2. Click the switch on the right-hand side to turn Ads on, then answer a few questions about the game you are making.  
![Enable Ads](../uploads/UnityAds/enableAds.png)

Ads are now enabled for your game.

##Step 2: Add code to your game

You can use code samples to implement ads in your game. Go to  the __Code samples__ tab and copy the relevant script snippets to your C# code (for example, during the loading scene or at the end of your game).

![Add Code](../uploads/UnityAds/addCode.png)

There are code samples for:

* __Simple__: Easy to use for simple fullscreen interstitial ads (for example, to appear between game levels)
* __Rewarded__: Show an ad with a result callback. You can use this to give your players in-game rewards (such as coins, gems, points or extra lives) for watching an ad.

### If you have previously used Unity Ads using the Asset Store package: what has changed?

* You do not need to register to Unity Ads' self-serve admin; instead, an account is created for you (if you don’t already have one) when you first enable ads in the editor.
* You do not need to create game profiles in self-server admin; game profiles and IDs will be created automatically when you enable ads in your project.
* You don’t need to initialise the ads system in your code, initialisation happens in the background.
* API changes: function names have been changed to be in line with normal C# naming conventions. (for example, `isReady` has been changed to `IsReady`). Also, the pause option has been removed as it was only used for picture ads.
* Support for picture ads has been removed