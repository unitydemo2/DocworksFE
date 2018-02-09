# Configuring for CloudMoolah Moo Store

## Introduction

This guide describes the process of establishing the digital records and relationships necessary for a Unity game to interact with an In-App Purchase Store. The [Unity IAP](https://docs.unity3d.com/Manual/UnityIAP.html) purchasing API is targeted.

In-App Purchase (IAP) is the process of transacting money for digital goods. A platform’s Store allows purchase of Products, representing digital goods. These Products have an Identifier, typically of string data type. Products have Types to represent their durability: *subscription*, *consumable* (capable of being rebought), and *non-consumable* (capable of being bought only once) are the most common.

## CloudMoolah Moo Store

CloudMoolah Developer Portal website: [dev.cloudmoolah.com](http://dev.cloudmoolah.com/) 

### Getting started

1. Write a game implementing Unity IAP. See [Unity IAP Initialization](https://docs.unity3d.com/Manual/UnityIAPInitialization.html) and [Integrating Unity IAP with your game](https://unity3d.com/learn/tutorials/topics/analytics/integrating-unity-iap-your-game-beta).
2. Keep the game’s product identifiers to hand for use in the Moo Store later. Note that the appKey and hashKey are discussed later in this document.
![](../uploads/Main/Configuring%20for%20CloudMoolah%20Moo%20Store_image_0.png)
3. Configure the Android target to CloudMoolah to ensure that store is accessed when a purchase is attempted. Alternatively, call the Editor API: ```UnityPurchasingEditor.TargetAndroidStore(AndroidStore.CloudMoolah);```
![](../uploads/Main/Configuring%20for%20CloudMoolah%20Moo%20Store_image_1.png)
4. After initialization of Unity IAP, inside the game’s [IStoreListener.OnInitialized](https://docs.unity3d.com/Manual/UnityIAPInitialization.html) implementation, add digital wallet integration. Do this by adding calls to IMoolahExtensions. Register prototyping the password with Unity’s [SystemInfo.deviceUniqueIdentifier](https://docs.unity3d.com/ScriptReference/SystemInfo-deviceUniqueIdentifier.html), collecting the username result string and passing that as well as the password into IMoolahExtensions.Login. See the scripting documentation in the [CloudMoolah Store](UnityIAPMoolahConfiguringMooStore) for further discussion of registration and login.
5. Build a signed non-Development Build Android APK from your game. See documentation on [getting started with Android development](https://docs.unity3d.com/Manual/android-GettingStarted.html) to learn more.

__Tip:__ Take special precautions to safely store your keystore file. The original keystore is always required to update a published application.

### Register the application

Register the application at the CloudMoolah Developer Portal website: [http://dev.cloudmoolah.com/](http://dev.cloudmoolah.com/)

1. Choose __Add New App__![](../uploads/Main/Configuring%20for%20CloudMoolah%20Moo%20Store_image_2.png)

2. Input game server information if defining an "Online" connected game.![](../uploads/Main/Configuring%20for%20CloudMoolah%20Moo%20Store_image_3.png)

![](../uploads/Main/Configuring%20for%20CloudMoolah%20Moo%20Store_image_4.png)

|**Property** |**Function** |
|:---|:---|
| __DataFeedURL_Stage__ |URL for redemption - test environment.|
| __DataFeedURL_Prod__ |URL for redemption - production environment.|
| __Testing Account__ |Account name for test environment.|
| __Testing Password__ |Password for test environment.|

3. Copy the appKey and hashKey into your application
![](../uploads/Main/Configuring%20for%20CloudMoolah%20Moo%20Store_image_5.png)

### Add In-App Purchases (IAP)

Add in-app purchases for this application at the CloudMoolah Developer Portal ([dev.cloudmoolah.com](http://dev.cloudmoolah.com/)).

1. Choose Add New Item![](../uploads/Main/Configuring%20for%20CloudMoolah%20Moo%20Store_image_6.png)

### Test IAP

The CloudMoolah Game Store supports testing via enabling a "Developer mode" in the app before making purchases. This special build of the game provides a fake offline store which performs performs fake purchases. This does not incur real-world monetary costs related to the product, and allows you to test the app’s purchasing logic.

Modify the game’s Unity IAP integration, adding the following line after creating the ConfigurationBuilder instance, then build and run the app, testing its in-app purchasing logic: 

```builder.Configure<IMoolahConfiguration>().SetMode(CloudMoolahMode.AlwaysSucceed); // TESTING: auto-approves all transactions``` 

You can also configure this to fail all transactions for testing error handling via the CloudMoolahMode.AlwaysFailed enumeration.

__Note:__ When testing is complete, make sure you remove the SetMode line disable Developer mode by using the CloudMoolahMode.Production enumeration. This ensures users pay real-world money when the app is in use.

