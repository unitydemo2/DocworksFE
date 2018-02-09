iOS & Mac App Stores
====================

Extended Functionality
----------------------

### Reading the App Receipt

An [App Receipt](https://developer.apple.com/library/ios/releasenotes/General/ValidateAppStoreReceipt/Chapters/ValidateRemotely.html) is stored on the device's local storage and can be read as follows:

````
var builder = ConfigurationBuilder.Instance(StandardPurchasingModule.Instance());
string receipt = builder.Configure<IAppleConfiguration>().appReceipt;
````

### Checking for payment restrictions

In App Purchases may be restricted in a device's settings, which can be checked for as follows:

````
var builder = ConfigurationBuilder.Instance(StandardPurchasingModule.Instance());
bool canMakePayments = builder.Configure<IAppleConfiguration>().canMakePayments;
````

### Restoring Transactions

On Apple platforms users must enter their password to retrieve previous transactions so your application must provide users with a button letting them do so. During this process the ``ProcessPurchase`` method of your ``IStoreListener`` will be invoked for any items the user already owns.

````
/// <summary>
/// Your IStoreListener implementation of OnInitialized.
/// </summary>
public void OnInitialized(IStoreController controller, IExtensionProvider extensions)
{
	extensions.GetExtension<IAppleExtensions> ().RestoreTransactions (result => {
		if (result) {
			// This does not mean anything was restored,
			// merely that the restoration process succeeded.
		} else {
			// Restoration failed.
		}
	});
}
````

### Refreshing the App Receipt

Apple provides a mechanism to fetch a new App Receipt from their servers, typically used when no receipt is currently cached in local storage; [SKReceiptRefreshRequest](https://developer.apple.com/library/ios/documentation/StoreKit/Reference/SKReceiptRefreshRequest_ClassRef/index.html#//apple_ref/occ/cl/SKReceiptRefreshRequest).

Note that this will prompt the user for their password.

Unity IAP makes this method available as follows:

````
/// <summary>
/// Your IStoreListener implementation of OnInitialized.
/// </summary>
public void OnInitialized(IStoreController controller, IExtensionProvider extensions)
{
	extensions.GetExtension<IAppleExtensions> ().RefreshAppReceipt (receipt => {
		// This handler is invoked if the request is successful.
		// Receipt will be the latest app receipt.
		Console.WriteLine(receipt);
	},
	() => {
		// This handler will be invoked if the request fails,
		// such as if the network is unavailable or the user
		// enters the wrong password.
	});
}
````

### Ask to Buy

iOS 8 introduced a new parental control feature;  [Ask to Buy](https://developer.apple.com/library/ios/technotes/tn2259/_index.html#//apple_ref/doc/uid/DTS40009578-CH1-UPDATE_YOUR_APP_FOR_ASK_TO_BUY)

Ask to buy allows an In App Purchase to be deferred to a parent for approval. When this occurs, Unity IAP will send your App a notification if it registers to be notified as follows.

````
/// <summary>
/// This will be called when Unity IAP has finished initialising.
/// </summary>
public void OnInitialized(IStoreController controller, IExtensionProvider extensions)
{
    extensions.GetExtension<IAppleExtensions>().RegisterPurchaseDeferredListener(product => {
        Console.WriteLine(product.definition.id);
    });
}
````

If and when the purchase is approved or rejected, the normal ProcessPurchase/OnPurchaseFailed methods of your store listener will be invoked.

Testing
-------

To test on Apple stores you must be using an iTunes connect test account, which can be created in iTunes connect.

Sign out of the app store on the iOS device or laptop, launch your application and you will be prompted to log in when you attempt either a purchase or to restore transactions.

If you receive an initialization failure with a reason of ``NoProductsAvailable``, follow this checklist:

* iTunes Connect product identifiers must exactly match the product identifiers supplied to Unity IAP
* In-App purchases must be enabled for your application in iTunes Connect
* Products must be cleared for sale in iTunes Connect
* It may take many hours for newly created iTunes Connect products to be available for purchase
* You must agree to the latest iTunes Connect developer agreements and have active bank details

Mac App Store
-------------

When building a desktop Mac build you must select ``Mac App Store validation`` within Unity’s build settings.

Once you have built your App, you must update its info.plist file with your bundle identifier and version strings. Right click on the ``.app`` file and click ``show package contents``, locate the ``info.plist`` file and update the ``CFBundleIdentifier`` string to your application's bundle identifier.

You must then sign, package and install your application. You will need to run the following commands from an OSX terminal:

````
codesign -f --deep -s "3rd Party Mac Developer Application: " your.app/Contents/Plugins/unitypurchasing.bundle
codesign -f --deep -s "3rd Party Mac Developer Application: " your.app
productbuild --component your.app /Applications --sign "3rd Party Mac Developer Installer: " your.pkg
````

To sign the bundle, you may first need to remove the Contents.meta file if it exists: `your.app/Contents/Plugins/unitypurchasing.bundle/Contents.meta`

In order to install the package correctly you must delete the unpackaged .app file before running the newly created package.

You must then launch your App from the Applications folder. The first time you do so, you will be prompted to enter your iTunes account details, for which you should enter your iTunes Connect test user account login. You will then be able to make test purchases against the sandbox environment.