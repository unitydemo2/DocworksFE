# Configuring for CloudMoolah MOO Store
 
## Introduction
 
This guide describes the process of establishing the digital records and relationships necessary for a Unity game to interact with an in-app purchase store.
 
In-app purchase (IAP) is the process of transacting money for digital goods inside an application. A platform’s store allows users to purchase products, which are digital goods. These products have an identifier, which is typically a string data type. 
 
Products have types to represent their durability:
 
* __Subscription:__ The player can buy the product again after the subscription term expires.
* __Consumable:__ The player can buy the same product multiple times.
* __Non-consumable:__ The player can only buy the product once.
 
## CloudMoolah MOO Store
 
Like the Apple App Store and the Google Play Store, the [CloudMoolah MOO Store](http://www.cloudmoolah.com/index.php/moo-store/) is a commercial online service that enables people to buy and sell mobile apps, and buy items in the application.
 
The MOO Store serves Asian markets. Users maintain a digital wallet, which they can top up using a variety of payment providers, such as banks and convenience store pre-paid cards.
 
The CloudMoolah Developer Portal website is at [dev.cloudmoolah.com](http://dev.cloudmoolah.com/). 
 
### Getting started
 
1. Make a game that implements Unity In-App Purchasing (see [Unity In-App Purchasing Initialization](https://docs.unity3d.com/Manual/UnityIAPInitialization.html) and [Integrating Unity In-App Purchasing with your game](https://unity3d.com/learn/tutorials/topics/analytics/integrating-unity-iap-your-game-beta) for more information). 
 
2. Keep the game’s product identifiers on hand for use in the MOO Store later (this document discusses `appKey` and `hashKey` later).
 
    This example configures and starts initialization of Unity In-App Purchasing:
 
```
    using UnityEngine.Purchasing;
    public class MyStore : IStoreListener {
 
	    public void InitializeStore() {
		    var module = StandardPurchasingModule.Instance();
		    var builder = ConfigurationBuilder.Instance(module);
 
		    builder.Configure<IMoolahConfiguration>().appKey = "d93f4564c41d463ed3d3cd207594ee1b";
		    builder.Configure<IMoolahConfiguration>().hashKey = "cc";
	    	builder.Configure<IMoolahConfiguration>().SetMode(CloudMoolahMode.Production);
	    	builder.AddProduct("100.gold.coins", ProductType.Consumable);
 
	    	UnityPurchasing.Initialize(this, builder);
    	}
    }
```
 
3. In the Unity Editor, configure the Android target to CloudMoolah to ensure that store is accessed when a purchase is attempted: <br/>Install the [Unity In-App Purchasing package](UnityIAPSettingUp), then find the Unity In-App Purchasing menu in Unity's Window menu: __Window__ > __Unity IAP__ > __Android__ > __Target CloudMoolah__. This ensures that, when the app is run on the Android operating system, it uses the CloudMoolah API to fulfill in-app purchase requests.
 
    ![](../uploads/Main/ConfiguringforCloudMoolahMooStore_image_1.png)
 
    Alternatively, call the Unity Editor API: ```UnityPurchasingEditor.TargetAndroidStore(AndroidStore.CloudMoolah);```
 
4. When the game successfully completes initialization of Unity In-App Purchasing, bind to the user’s Cloud Moolah digital wallet with the `IMoolahExtension.FastRegister` and `IMoolahExtension.Login` API. In the game’s implementation of [IStoreListener.OnInitialized](https://docs.unity3d.com/Manual/UnityIAPInitialization.html), use the `IMoolahExtension.FastRegister` API to register a new digital wallet for the user, and the `IMoolahExtension.Login` API to access a user’s existing wallet. <br/><br/>
 
    `IMoolahExtension.FastRegister` requires a user identifying string `cmPassword`. This string is also required by the `Login` API to unlock that user’s digital wallet, and their collection of owned IAP products. Ensure the string identifies this user uniquely for your application. Collect FastRegister’s `cmUserName` result, and use that in subsequent calls to `IMoolahExtension.Login`. Save this `cmUserName` on your backend server, if available, or in PlayerPrefs.
 
    See the scripting documentation in the [CloudMoolah Store](UnityIAPMoolahMooStore) for further discussion of registration and login.
 
5. Build a signed non-Development Build Android APK from your game. See documentation on [getting started with Android development](https://docs.unity3d.com/Manual/android-GettingStarted.html) to learn more about this.
 
__Tip:__ Take special precautions to safely store your keystore file. The original keystore is always required to update a published app.
 
### Register the app
 
Register the app at the CloudMoolah Developer Portal website ([dev.cloudmoolah.com](http://dev.cloudmoolah.com/)). 
 
1. Choose __Add New App__.
    ![](../uploads/Main/ConfiguringforCloudMoolahMooStore_image_2.png)
 
2. Input game server information if you are defining a game that is connected to the internet.
 
    ![Input server information](../uploads/Main/ConfiguringforCloudMoolahMooStore_image_3.png)
 
    ![Input server information as shown in the table below](../uploads/Main/ConfiguringforCloudMoolahMooStore_image_4.png)
 
    |**Property** |**Function** |
    |:---|:---|
    | __DataFeedURL_Stage__ |URL for redemption - test environment.|
    | __DataFeedURL_Prod__ |URL for redemption - production environment.|
    | __Testing Account__ |Account name for test environment.|
    | __Testing Password__ |Password for test environment.|
 
3. Copy the appKey and hashKey into your app
 
        ![](../uploads/Main/ConfiguringforCloudMoolahMooStore_image_5.png)
 
### Add in-app purchases (IAP)
 
At the CloudMoolah Developer Portal ([dev.cloudmoolah.com](http://dev.cloudmoolah.com/)), select __Add New Item__ to add in-app purchases for this app.
 
![](../uploads/Main/ConfiguringforCloudMoolahMooStore_image_6.png)
 
### Test IAP
 
The CloudMoolah Game Store supports testing. Enable developer mode in the app before making purchases (do this via `IMoolahConfiguration.SetMode` API - see below). This special build of the game provides a fake offline store which performs performs fake purchases. This does not incur real-world monetary costs related to the product, and allows you to test the app’s purchasing logic.
 
To modify the game’s MOO Store test mode, create the `ConfigurationBuilder` instance and add the following line, then build and run the app to test its in-app purchasing logic: 
 
```
builder.Configure<IMoolahConfiguration>().SetMode(CloudMoolahMode.AlwaysSucceed); // TESTING: auto-approves all transactions
``` 
 
To test error handling, configure this to fail all transactions. To do this, use tthe `CloudMoolahMode.AlwaysFailed` enumeration. For example:
 
```
builder.Configure<IMoolahConfiguration>().SetMode(CloudMoolahMode.AlwaysFailed); // TESTING: always fails all transactions
```
 
__Note:__ When you have finished testing, make sure you remove the `SetMode` line that disables Developer mode, and use the `CloudMoolahMode.Production` enumeration. This ensures users pay real-world money when the app is in use.

<br/>
<br/>
--------
*  <span class="page-edit">2017-07-03  <!-- include IncludeTextAmendPageSomeEdit --></span>
*  <span class="page-history">2017-07-03 - Documentation only update</span>