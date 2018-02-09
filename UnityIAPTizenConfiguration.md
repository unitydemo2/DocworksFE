# Configuring for Tizen Store

This page describes the process of establishing the digital records and relationships necessary for a Unity game to interact with an in-app purchase store. The [Unity IAP](UnityIAP) purchasing API is targeted.

In-app purchasing (IAP) is the process of transacting money for digital goods. A platform’s store allows the purchase of products, representing digital goods. These products have an identifier, typically a string datatype. Products have types to represent their durability: the most common are consumable (capable of being rebought), and non-consumable (capable of being bought once). The Tizen Seller Store (also known as the Tizen Store) is limited to consumable and non-consumable products.

## Tizen Store

### Getting started

1. Write a game implementing Unity IAP functionality. See documentation on [Unity IAP Initialization](UnityIAPInitialization) and the tutorial on [Integrating Unity IAP In Your Game](https://unity3d.com/learn/tutorials/topics/analytics/integrating-unity-iap-your-game) for help getting started with this. You may wish to refer to the IAP Demo test scene and script (installed when the Purchasing package is imported) to familiarize yourself with the environment and simplify the initial Tizen Seller Store item setup.

2. This guide assumes that you already have a Commercial Tizen Seller Office account set up, and are familiar with adding applications to the Tizen Seller Store. For more details, see the [Tizen Seller Office Guide Download](http://seller.tizenstore.com/info/guideDownload.as) sections on Commercial Seller Request Guide and Seller Office Guide for In-App Purchase. Note that you must be logged in to an account at [Tizen Store: Seller Office](https://seller.tizenstore.com) in order to access these documents. To access the **Item** sub-menu required to set up IAP, you need to set up a Commercial account. 


![Tizen Seller Store sign-in](../uploads/Main/Image0.png)


The basic steps for IAP integration are explained in the sections below, in the following order:

1. Register the application

2. Set up the IAP items

3. Test

4. Deploy

### Register the application

Register the Tizen application with the [Tizen Store: Seller Office](http://seller.tizenstore.com/).

1. Request a commercial account if you do not already have one. This may take a day or longer to complete. See the documentation at [Tizen Seller Office Guide Download](http://seller.tizenstore.com/info/guideDownload.as) for more information.

2. Choose __Add New Application__ and enter the application title and default language.

3. Click __Upload a new binary__ and upload your `.tpk` file. Note that if you need to update the binary later, you will also need to update the version number of your game in Unity before creating the new build. 


![](../uploads/Main/Image1.png)


4. Provide any additional required information on the __Binary__ tab, then click on the __Save__ button. Note that the Tizen Seller Store UI may respond with *Application information is saved successfully*, even if there is missing information on the page. 


![The Tizen Seller Store UI may respond with this message, even if there is missing information on the page](../uploads/Main/Image2.png)

5. Complete the required information on the __Sales__ and __Display__ tabs. A green check appears on each tab (except __Item__) when the necessary data is complete. 


![](../uploads/Main/Image3.png)


### Add in-app purchases

In the [Tizen ](http://seller.tizenstore.com)[Seller Office](http://seller.tizenstore.com), add the in-app purchases for your game.

1. First, select **Add Item Group**: A unique **Item Group ID** is generated for you.


![](../uploads/Main/Image4.png)

![](../uploads/Main/Image5.png)


2. Add one or more items to the item group. The Tizen Seller Store generates a unique **Item ID** (currently 12-character numeric strings such as `000000596733`) for each item. To simplify cross-platform purchasing, use the Tizen Seller Store __Item ID__ as a store-specific ID when adding the product to your application (see documentation on [Defining products](UnityIAPDefiningProducts) for more information).

3. Review your list of items in the Tizen Seller Store. 


![](../uploads/Main/Image6.png)

4. Use the store-specific IDs in your script’s calls to the Unity IAP `ConfigurationBuilder.AddProduct` function when defining which products will be available in your app.

### Test IAP

Unity IAP for Tizen supports testing via the __Beta Test__ mode on the Tizen Seller Store. Applications under beta test allow transactions to proceed, but do not incur actual charges. You need to manually add Beta testers to your application on the __Beta Test__ tab. 


![](../uploads/Main/Image7.png)

See Tizen’s [Beta Test Guide](http://seller.tizenstore.com/info/guideDownload.as) documentation for additional details. 

Note that it can take some time between when you start the beta test and when the application becomes available to your beta testers. At the point that the application becomes available to your beta testers, your IAP items are also available for purchase.

