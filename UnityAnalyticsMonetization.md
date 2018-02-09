Monetization
============

Unity Analytics allows you to monitor your in-game revenue from monetization. By implementing [receipt verification](UnityAnalyticsReceiptVerification) you'll quickly see legitimate or fraudulent transactions.

Unity Analytics provides the __Analytics.Transaction__ method for tracking monetization events through in-app purchases. This method should be called every time a player triggers a monetization event. The __Analytics.Transaction__ method requires a price parameter, a currency and an optional Apple iTunes / Google Play receipt string.


````
  // Reference the Unity Analytics namespace
  using UnityEngine.Analytics;

  // Use this call for each and every place that a player triggers a monetization event
  Analytics.Transaction(string productId, decimal price,
  string currency, string receipt,
  string signature);
````
|**_Analytics.Transaction Input Parameters_**|||
|**_Name_** |**_Type_** |**_Description_** |
|:---|:---|
|__productId__ |string |The id of the purchased item. |
|__price__ |decimal |The price of the item. |
|__currency__ |string |Abbreviation of the currency used for the transaction. For example "USD" (United States Dollars). See [here](http://en.wikipedia.org/wiki/ISO_4217) for a standardized list of currency abbreviations. |
|__receipt__ |string |Receipt data (iOS) or receipt ID (Android) for in-app purchases to verify purchases with Apple iTunes or Google play.  Use __null__ in the absence of receipts. For more details see [Receipt Verification](UnityAnalyticsReceiptVerification). |
|__signature__ |string | Android receipt signature.  If using native Android use the __INAPP_DATA_SIGNATURE__ string containing the signature of the purchase data that was signed with the private key of the developer.  The data signature uses the RSASSA-PKCS1-v1_5 scheme. Pass in __null__ in the absence of a signature. |

The example below is for a $0.99 transaction in USD without receipt validation.

````
Analytics.Transaction("12345abcde", 0.99m, "USD", null, null);
````

Press Play 
----------
To send test Monetization data to our servers and validate your integration, trigger a purchase during Editor Play mode. If integration is successful, your test data will display in the table below.

![](../uploads/Main/AnalyticsPlayGame.gif)

Validate
--------
![](../uploads/Main/AnalyticsValidate.png)
