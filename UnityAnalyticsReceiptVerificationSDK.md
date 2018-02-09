Receipt Verification
====================
Here are the implementation details:
 
###For iOS

####__receipt__ parameter
* If you leave this as __null__, this transaction will show up in Unverified Revenue
* If you are writing a Native iOS plugin
    * For iOS 6 and below, send the raw SKPaymentTransaction's [transactionReceipt](https://developer.apple.com/library/ios/documentation/StoreKit/Reference/SKPaymentTransaction_Class/#//apple_ref/occ/instp/SKPaymentTransaction/transactionReceipt)
    * For iOS 7 and above, send the [base64 encoded value of the App Receipt](https://developer.apple.com/library/ios/releasenotes/General/ValidateAppStoreReceipt/Chapters/ValidateRemotely.html) from the app bundle. 
* If you are using Unibill plugin
    * Pass in [PurchasableItem's "receipt" property](http://outlinegames.com/unibill-documentation/#toc-purchasableitem) as the receipt. 
* If you are using Prime31 plugin
    * Pass in StoreKitTransaction's "base64EncodedTransactionReceipt" property as the receipt.

####__signature__ parameter
Pass in __null__ since this is not used.


###For Android
To validate Android monetization, please enter your Google Public API Key in your Analytics dashboard Project Settings Form. 

The Google Public API Key is needed for implementing receipt verification for in-app purchases (IAP) on Google Play. Your Google Public Key is under Google Play Developer console > All applications > Services & APIs > Your License Key For This Application. This is optional, but if you are developing for Android and have in-app purchases, we highly recommend implementing it. 

####__receipt__ parameter
* If you leave this as null, this transaction will show up as Unverified Revenue
* If you are writing a Native Android plugin
    * Pass in the the [purchase data](http://developer.android.com/google/play/billing/billing_integrate.html) for the order, which is a String in JSON format that is mapped to the INAPP_PURCHASE_DATA key in the response Intent. 
* If you are using Unibill plugin
    * Parse the [PurchasableItem's "receipt" property](http://outlinegames.com/unibill-documentation/#toc-google-play) as JSON, and pass in the value of the "json" property. 
* If you are using Prime31 plugin
    * Pass in GooglePurchase "originalJson" property
  
####__signature__ parameter
* If you leave this as __null__, this transaction will show up as Unverified Revenue
* If you are writing a Native Android plugin
    * Pass in the the [signature](http://developer.android.com/google/play/billing/billing_integrate.html), which is mapped to the INAPP_DATA_SIGNATURE key in the response Intent. 
* If you are using Unibill plugin
    * Parse the [PurchasableItem's "receipt" property as JSON](http://outlinegames.com/unibill-documentation/#toc-google-play), and pass in the value of the signature property. 
* If you are using Prime31 plugin
    * Pass in GooglePurchase "signature" property.