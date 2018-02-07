# Defining products
Your application must provide a list of products for sale. This can be done in your Application with code.

## Product Types

Each product must be of one of the following Types:

| | |
|:---|:---|
|__Consumable__|Can be purchased repeatedly. Suitable for consumable items such as virtual currencies. Cannot be restored.|
|__NonConsumable__|Can only be purchased once. Suitable for one-off purchases such as extra levels. Restorable.|
|__Subscription__|Has a finite window of validity. Restorable.|

## Defining products directly in your App

You can declare your product list programmatically using the [ConfigurationBuilder](http://docs.unity3d.com/ScriptReference/Purchasing.ConfigurationBuilder.html).

A unique cross-store identifier must be supplied for all products, and one of the aforementioned types.

````
using UnityEngine;
using UnityEngine.Purchasing;

public class MyIAPManager {
    public MyIAPManager () {
        var builder = ConfigurationBuilder.Instance(StandardPurchasingModule.Instance());
        builder.AddProduct("100_gold_coins", ProductType.Consumable);
        // Initialize Unity IAP...
    }
}
````

### Store specific IDs

By default Unity IAP assumes that your product has the same identifier across all the App stores.

For example, in the previous example, Unity IAP would use an ID of "100_gold_coins" when communicating with every App store.

There are occasions when it is not possible to reuse the same product identifier across every store, such as when publishing to both iOS & Mac stores which prohibit developers from using the same product ID across both.

In these situations a mechanism is provided to tell Unity IAP the product's correct identifier where it differs from the cross-platform ID.

````
using UnityEngine;
using UnityEngine.Purchasing;

public class MyIAPManager {
    public MyIAPManager () {
        var builder = ConfigurationBuilder.Instance(StandardPurchasingModule.Instance());
        builder.AddProduct("100_gold_coins", ProductType.Consumable, new IDs
        {
            {"100_gold_coins_google", GooglePlay.Name},
            {"100_gold_coins_mac", MacAppStore.Name}
        });
        // Initialize Unity IAP...
    }
}
````

In this example the product is known as "100_gold_coins_google" on Google Play and "100_gold_coins_mac" on the Mac App store.

It is recommended that you reuse the same product identifiers across all stores where possible.

Note that defining store-specific identifiers changes only the identifier Unity IAP uses when communicating with stores; you should continue to use the product's cross-platform identifier when making API calls.
