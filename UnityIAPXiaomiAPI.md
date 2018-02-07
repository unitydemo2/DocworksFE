#Unity Channel SDK and API extensions

##Unity Channel API
###UnityEngine.Store namespace
####AppInfo class
The ```AppInfo``` class stores client and Xiaomi credentials needed for client-to-server communication and authentication.

|**Key:** |**Type:** |**Description:** |
|:---|:---|:---|
|__appID__|string|Xiaomi app ID|
|__appKey__|string|Xiaomi app key|
|__clientID__|string|Unity client ID|
|__clientKey__|string|Unity client key|
|__debug__|bool|Toggle debug mode|

####ILoginListener interface
Xiaomi requires login through the ```ILoginListener``` for all apps publishing to the Mi Game Center.

|**Key:** |**Type:** |**Description:** |
|:---|:---|:---|
|__OnInitialized ()__|void|Called when initialization succeeds|
|__OnInitializedFailed (string message)__|void|Called when initialization fails|
|__OnLogin ()__|void|Called when login succeeds|
|__OnLoginFailed (string message)__|void|Called when login fails|

####StoreService class
Unity IAP uses the ```StoreService``` class internally to initialize the Unity Channel SDK.

|**Key:** |**Type:** |**Description:** |
|:---|:---|:---|
|__static Initialize (AppInfo appInfo, ILoginListener loginListener)__|void|Initialize the Unity Channel SDK|
|__static Login (AppInfo appInfo, ILoginListener loginListener)__|void|Login to the Xiaomi account|

####UserInfo class
A successful login to Unity Channel returns the ```UserInfo``` class. The data returned is for informational purposes.  

|**Key:** |**Type:** |**Description:** |
|:---|:---|:---|
|__channel__|string|Indicates which channel you are using (currently, it is only “XIAOMI”)|
|__userID__|string|Channel’s unique user ID|
|__userLoginToken__|string|Validate the user login (see Server-side initialization section of Xiaomi IAP integration guide)|

###UnityEngine.ChannelPurchase namespace
####IPurchaseListener interface
Unity IAP uses the ```IPurchaseListener``` interface internally to handle purchasing activities.

Implement the ```IPurchaseListener``` class to handle states of the purchase flow:

```
using UnityEngine.ChannelPurchase;
......
private class ExamplePurchaseListener : IPurchaseListener{
    public void OnPurchase (PurchaseInfo purchaseInfo){
        Debug.Log ("Purchase Succeed: " + purchaseInfo.gameOrderId);
    }
    public void OnPurchaseFailed (string message, PurchaseInfo purchaseInfo){
        Debug.Log ("Purchase Failed: " + message);
    }
    public void OnPurchaseRepeated(string productCode){
        Debug.Log ("Purchase Repeated");
    }
    public void OnReceiptValidate (ReceiptInfo receiptInfo){
        Debug.Log ("Validate Succeed");
    }
    public void OnReceiptValidateFailed (string gameOrderId, string message){
        Debug.Log ("Validate Failed");
    }
    public void OnPurchaseConfirm (string gameOrderId){
        Debug.Log ("Confirm Succeed");
    }
    public void OnPurchaseConfirmFailed (string gameOrderId, string message){
        Debug.Log ("Confirm Failed");
    }
}
```
|**Key:** |**Type:** |**Description:** |
|:---|:---|:---|
|__OnPurchase ()__|void|Called when purchase succeeds|
|__OnPurchaseFailed (string message, PurchaseInfo purchaseInfo)__|void|Called when purchase fails|
|__OnPurchaseRepeated (string productCode)__|void|Called when non-consumable Products are re-purchased|
|__OnReceiptValidation (ReceiptInfo receiptInfo)__|void|Called when ```PurchaseService.ValidateReceipt (...)``` succeeds|
|__OnReceiptValidationFailed (string gameOrderID, string message)__|void|Called when ```PurchaseService.ValidateReceipt (...)``` fails|
|__OnPurchaseConfirm (string gameOrderId)__|void|Deprecated|
|__OnPurchaseConfirm (string gameOrderId, string message)__|void|Deprecated|

####PurchaseService class
Unity IAP uses the ```PurchaseService``` class internally to initiate purchasing activities.

With the purchase listener implemented, call the ```PurchaseService.Purchase``` method to execute a purchase transaction:

```
using UnityEngine.ChannelPurchase;
......
    var myPurchaseListener = new ExamplePurchaseListener ();    
    PurchaseService.Purchase ("Product ID", "Game Order ID", myPurchaseListener);
```

Product IDs are listed in the Xiaomi developer portal. If your app runs in debug mode, Product IDs also export to the _MiGameProductCatalog.prop_ file. Game Order ID can be null; the Unity Channel SDK will generate its UUID.

|**Key:** |**Type:** |**Description:** |
|:---|:---|:---|
|__static Purchase (string productCode, string gameOrderId, IPurchaseListener productListener)__|void|Purchase Products|
|__static ValidateReceipt (string gameOrderId, IPurchaseListener purchaseListener)__|void|Validate purchase|
|__static ConfirmPurchase ()__|void|Deprecated (use ```ValidateReceipt (...)``` instead)|

####PurchaseInfo class
After a purchase, validate it by calling the ```PurchaseService.ValidateReceipt``` method:

```
    PurchaseService.ValidateReceipt(gameOrderId, myPurchaseListener);
```

If ```gameOrderId``` is valid, ```myPurchaseListener``` receives ```ReceiptInfo``` containing ```signData``` and ```signature```, which Unity Channel uses to validate the purchase.

|**Key:** |**Type:** |**Description:** |
|:---|:---|:---|
|__productCode__|string|A Product’s unique ID (you can also configure this directly in the Xiaomi dev portal)|
|__gameOrderId__|string|The order’s purchase ID|
|__orderQueryToken__|string|Used to validate purchases|

<a name="ReceiptInfo"></a>
####ReceiptInfo class
Validation usually occurs on the game server, however you can also validate the ```signData``` client-side.

|**Key:** |**Type:** |**Description:** |
|:---|:---|:---|
|__gameOrderId__|string|The order’s purchase ID|
|__signData__|string|A JSON string containing details of the purchase|
|__signature__|string|signData’s signature|

##Receipt validation and extensions API
Before continuing, please review documentation on [Unity IAP receipt validation](https://docs.unity3d.com/Manual/UnityIAPValidatingReceipts.html). Also see the [UnityEngine.Purchasing Scripting API](https://docs.unity3d.com/ScriptReference/index.html).

###UnityEngine.Purchasing namespace
The ```IUnityChannelConfiguration``` and ```IUnityChannelExtensions``` interfaces offer extended functionality for unpacking app store receipts.

Perform local receipt validation by using the Unity IAP ```CrossPlatformValidator``` class (detailed in the [Receipt validation](https://docs.unity3d.com/Manual/UnityIAPValidatingReceipts.html) documentation) and the ```IUnityChannelExtensions.ValidateReceipt``` method (detailed below) at the time of purchase.

Before implementing validation, enable receipt obfuscation for Xiaomi:

1. Obtain your app’s __Client RSA Public Key__ from your App Store Settings (see the **App Store Settings** section of the [Xiaomi IAP integration guide](https://docs.unity3d.com/Manual/UnityIAPXiaomi.html)), or from the [Unity Client Settings dashboard](https://id.unity.com/en/user_clients/settings).
2. In the Unity Editor, enter the Unity Channel key into the Unity IAP Receipt Validation Obfuscator window (__Window__ > __Unity IAP__ > __Receipt Validation Obfuscator__). This window collects, obfuscates, and stores public keys in the Project for receipt validation purposes.
3. In the Receipt Validation Obfuscator window, select __Obfuscate Unity Channel Public Key__ to save the resulting _UnityChannelTangle_ datafile to the Project.


![The Unity IAP Receipt Validation Obfuscator window. Generates data classes in the project for use with the CrossPlatformValidator.](../uploads/Main/ReceiptObfuscation.png)

####IUnityChannelConfiguration interface
To automatically fetch the required receipt data from Unity Channel during purchase, set ```IUnityChannelConfiguration.fetchReceiptPayloadOnPurchase``` to ```true``` when initializing Unity IAP. This calls ```IUnityChannelExtensions.ValidateReceipt``` internally after a successful purchase (ideally when the [```PurchaseEventArgs```](https://docs.unity3d.com/ScriptReference/Purchasing.PurchaseEventArgs.html)’ ```purchasedProduct.receipt``` field triggers the ```IStoreListener.ProcessPurchase``` success callback).  

**Note**: Setting the ```fetchReceiptPayloadOnPurchase``` flag to true incurs a network request to fetch the cryptographic receipt data after a successful purchase. If this second network request fails for any reason, the ```ProcessPurchase``` success callback receives a Product with an invalid receipt.

Passing ```purchasedProduct.receipt``` data through the ```CrossPlatformValidator.Validate``` API returns an ```IPurchaseReceipt```, which is the fully validated receipt. If the result is empty, the validation failed. See the example below: 

```
CrossPlatformValidator validator = new CrossPlatformValidator (GooglePlayTangle.Data(), AppleTangle.Data(), UnityChannelTangle.Data(), Application.identifier);

var result = validator.Validate(purchasedProduct.receipt);
```

|**Key:** |**Type:** |**Description:** |
|:---|:---|:---|
|__fetchReceiptPayloadOnPurchase__|bool|Automates Unity Channel receipt data collection during purchase|

####IUnityChannelExtensions interface
Use the ```IUnityChannelExtensions``` interface to confirm purchases and validate receipts. The callbacks for the above methods return a bool indicating success, a ‘signData’ string, and a ‘signature’ string (see section on [ChannelPurchase.ReceiptInfo](#ReceiptInfo)).
 
**Note**: ```ValidateReceipt ()``` is vulnerable to [man-in-the-middle attacks](https://en.wikipedia.org/wiki/Man-in-the-middle_attack); use the Client RSA Public Key for added security (see the **App Store Settings** section of the [Xiaomi IAP integration guide](https://docs.unity3d.com/Manual/UnityIAPXiaomi.html)).

|**Key:** |**Type:** |**Description:** |
|:---|:---|:---|
|__`ConfirmPurchase (string transactionID, Action<bool, string, string>, callback)`__|void|Collects purchase status for a prior purchase (used to review purchase history, especially for game interruption or network timeouts)|
|__`ValidateReceipt (string transactionID, Action<bool, string, string>, callback)`__|void|Validates the receipt for a given transactionID|

####UnifiedReceipt class
The ```UnifiedReceipt``` class contains store-specific transaction data that Unity IAP can interpret. See the example below on how to unpack a unified receipt string:

```
var unifiedReceipt = JsonUtility.FromJson<UnifiedReceipt>(purchEvtArg.purchasedProduct.receipt)
```

|**Key:** |**Type:** |**Description:** |
|:---|:---|:---|
|__Payload__|string|Unity IAP’s wrapper for receipts that come back in different formats for different stores|
|__Store__|string|The store on which the purchase occurred|
|__TransactionID__|string|The unique transaction ID|

####UnityChannelPurchaseReceipt interface
Use the ```UnityChannelPurchaseReceipt``` to further unpack a unified receipt into a Unity Channel receipt. See the example below:

```
var ucReceipt = JsonUtility.FromJson<UnityChannelPurchaseReceipt>(unifiedReceipt.Payload)
```

Use this additional Unity Channel receipt data for informational purposes.

|**Key:** |**Type:** |**Description:** |
|:---|:---|:---|
|__productID__|string|The unique ID of the purchased Product|
|__transactionID__|string|The unique transaction ID|
|__orderQueryToken__|string|The order query token|

###Store identification at runtime
To check if the Xiaomi app store is the active store in your game at runtime, use the boolean value provided by the following code snippet:

```
var module = StandardPurchasingModule.Instance();
bool m_IsUnityChannelSelected = 
    Application.platform == RuntimePlatform.Android && 
    module.androidStore == AndroidStore.XiaomiMiPay;
```
