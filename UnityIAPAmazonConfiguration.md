# Configuration for the Amazon Appstore and Amazon Underground stores

##Introduction

This guide describes the process of setting up the Amazon Appstore and the Amazon Underground stores for use with the Unity in-app purchasing (IAP) system. This includes establishing the digital records and relationships that are required to interact with the Unity IAP API, setting up an Amazon developer account, and testing and publishing a Unity IAP application. 

As with other platforms, the Amazon stores allow for the purchase of virtual goods and managed products. These digital products are identified using a string identifier and an additional type to define durability, with choices including subscription (capable of being subscribed to), consumable (capable of being rebought), and non-consumable (capable of being bought once). Note that the Amazon Underground store does not support subscription.

Amazon has established two app stores for both non-FireOS Android devices as well as FireOS, set up to support free and paid versions of the same app: 

* The Amazon Appstore is provided to support paid and free apps. 
* The Amazon Underground store is designed to give developers a payment schedule for eligible free apps. The Underground store also has stringent [requirements](https://developer.amazon.com/public/solutions/underground/docs/amazon-underground-eligibility-and-submission-checklists) for apps based on pay per time spent in the application. More details can be found in the [program overview](https://developer.amazon.com/public/solutions/underground) and [details](https://developer.amazon.com/public/solutions/underground/docs/understanding-amazon-underground) documents.

##Cross-store implementation of in-app purchases

There are cross-store installation issues with publishing to multiple Android IAP stores (e.g. Amazon and Google) simultaneously and shared Android bundle identifiers. Please see the page on [Cross-store installation issues with Android in-app purchase stores](UnityIAPCrossStoreInstallationIssues) to learn more.

##Amazon Appstore and Amazon Underground stores

###Getting started

1. Set up an Amazon developer account at the [Amazon developer portal](https://developer.amazon.com/). A single developer account may be used to set up both stores.
1. Determine which store is most appropriate for your app. Take note of your game's product identifiers, and study the differences in the types of digital items that are acceptable for the different stores. For example, the identifier for consumable coins will be used in the Amazon store rather than the Amazon Underground store.
1. Write a game implementing the Unity IAP API. For reference, see the guides on [Unity IAP initialization](UnityIAPInitialization) and [Integrating Unity IAP in your game](https://unity3d.com/learn/tutorials/topics/analytics/integrating-unity-iap-your-game). Use the Amazon Appstore for apps with no restrictions on IAP items. To create a free version of your app for the Amazon Underground store, follow Amazon's guidelines.

###Device setup

1. For non-FireOS Android devices, download and install the [Amazon Appstore](https://www.amazon.com/appstore_android_app). Additionally, if you plan on an Underground version of your app, download and install the [Amazon Underground store](https://www.amazon.com/underground).
1. On FireOS devices, the Amazon Appstore and the Amazon Underground apps should come pre-installed. If your FireOS device doesn't have the Amazon Underground store installed, download and install it from the [Amazon website](https://www.amazon.com/underground). 
1. Once you have installed Amazon Appstore (and Amazon Underground, if desired), install the [Amazon App Tester](http://www.amazon.com/Amazon-App-Tester/dp/B00BN3YZM2/).

    ![](../uploads/Main/AmazonConfiguration-AmazonAppTester.png) 
1. Set up the Android SDK
    1. To install and watch the Android debug log, ensure you have the [Android SDK](https://developer.android.com/studio/install.html) installed. Download the relevant command line tools package from the Android SDK install page and extract them to your computer.
    1. Confirm that the SDK recognizes the attached Android device through the command-line adb tool. For example:
    
````
|[11:07:01] user@laptop:/Applications | $ adb devices
List of devices attached
00DA0807526300W5	device
````

###Unity app setup

Setting up to use Unity's IAP takes a few steps.

1. Import the Unity IAP plug-in. See [Setting up Unity IAP](UnityIAPSettingUp) for more information (Unity 5.3 or higher).
1. Set the IAP target store. You should already have an Android app set up. Set the target store using __Unity IAP's Window > Unity IAP > Android > Target Amazon__ menu item. This is used to toggle between Google and Amazon stores.

    ![](../uploads/Main/AmazonConfiguration-TargetAmazonMenu.png)

Alternatively, call the API: 

````
UnityPurchasingEditor.TargetAndroidStore(AndroidStore.AmazonAppStore)
````

###Amazon Appstore and Amazon Underground setup

It's not necessary to download Amazon's native IAP plug-in when preparing to use the Amazon stores, as all of the functionality it provides is already included in Unity's IAP service.

1. Add your app. From the Amazon Developer Portal select __Add a New App__.

    ![](../uploads/Main/AmazonConfiguration-AddNewApp.png)

1. Set up your catalog. Using the product descriptions you prepared earlier, add the items to the Amazon catalog using the Amazon Developer Portal. Navigate to your app's page, and find the __In-App Items section__. Use the __Add a Consumable__, __Add an Entitlement__, or __Add a Subscription__ buttons to set up your catalog.

    ![](../uploads/Main/AmazonConfiguration-SetUpCatalog.png)



