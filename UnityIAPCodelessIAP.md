# Codeless IAP

Codeless IAP is the easiest way to integrate in-app purchases in your Unity app. You can use the Unity Editor to set up basic IAP integration using minimal script writing.

Codeless IAP is "codeless" in that you don’t need write code to perform the actual IAP transaction. Once the IAP transaction is completed, you do need to define how users are granted access to their newly purchased product via scripting. However, you may not need to do scripting if, for example, you use a GameObject from the Asset Store with a suitable script for receiving messages that results in the user accumulating in-game wealth.

Note that you can access extended functionality through scripting - see [accessing Unity IAP’s extended functionality](#ExtendedFunctionality) below for more information.

For further information and the opportunity to give feedback and ask questions, visit the [Unity IAP forums](https://forum.unity3d.com/threads/ann-codeless-iap-for-unity-iap.443277/).

## Using Codeless IAP

Add IAP Buttons to your app and define your products in the IAP Catalog. Then, when players run your game, the Unity Purchasing system is configured based on the products you entered in the catalog. When a player taps or clicks on an IAP Button, it initiates a purchase of the associated product.

### Setup

__Note:__ Before following these guides, ensure you have the Unity IAP plugin installed. See documentation on [setting up Unity IAP](UnityIAPSettingUp) for more information.

![Image A: Inspector for a Button with the Codeless IAP component](../uploads/Main/CodelessIAPGettingStartedGuide_image_0.png)

1. To add an IAP Button to your Scene, in the Unity Editor menu, select __Window__ > __Unity IAP__ > __Create IAP Button__.

2. Select your new IAP Button GameObject in the Scene view and locate the __IAP Button (Script)__ component in the Inspector (see image A, above). Click the __IAP Catalog…__ button to open the IAP Catalog window (see image B, below). Alternatively, in the Unity Editor menu, select  __Window__ > __Unity IAP__ > __IAP Catalog__. 

    ![Image B: IAP Catalog window for defining and exporting products](../uploads/Main/UnityIAPCodelessIAP-1.png)

3. Define a product __ID__ for your IAP product. This ID identifies your product with the app stores. Note that you can override this ID with a unique store-specific ID through the __Advanced__ option.

4. Choose a product __Type__ (products can be __Consumable__, __Non-consumable__, or __Subscription__).

5. Select your IAP Button GameObject again in the Scene view, and locate the __IAP Button (Script)__ component in the Inspector (see image A, above) again.

6. Choose the product from the __Product ID__ pop-up.

7. Either create your own function that provides purchase fulfillment using scripting or import an Asset to do this. For example, you could import an Asset from the Asset Store with a suitable IAP function (script) for receiving messages that result in the user accumulating in-game wealth. 

To do this:

1. Apply your purchase fulfilment function (script) as a component to a GameObject.

2. Connect it to the __On Purchase Complete (Product)__ event field in the component’s Inspector (see Image A, above).

3. Select __+__ on the Inspector and and drag and drop your purchase fulfillment GameObject into the event field as shown in Image A.

Below is an example of a simple on-purchase success function (script). For demonstration purposes, it displays the text "You Got Money!" in the Unity Editor [Console Window](Console) on success. In your game, credit the user’s wallet with currency or add items to their inventory instead.

````
using UnityEngine;
using UnityEngine.Purchasing;

    public class DemoInventory : MonoBehaviour{
        public void Fulfill (Product product){
            if (product != null) {
                switch (product.definition.id){
                    case "100.gold.coins":
                        Debug.Log ("You Got Money!");
                        break;
                    default:
                        Debug.Log (
                        string.Format ("Unrecognized productId \"{0}\"",product.definition.id)
                            );
                        break;
                    }
                }
            }
        }
````

Finally, run your game to test the IAP Button.

See the Advanced section, below, for additional information on run time and export-related settings in the the IAP Catalog window. 

#### Advanced

![Image C: The IAP Catalog window with the Advanced section folded out](../uploads/Main/CodelessIAPGettingStartedGuide_image_1.png)

Access the Advanced section by clicking on the arrow icon next to __Advanced__ in the IAP Catalog window.

Advanced fields customize a product with store-specific detail. You can fill out the advanced fields to provide a title and description for your IAP products, override a product’s ID for a particular store, and provide pricing information. After providing this information, you can export the catalog.

**Runtime-related functions**<br/>
To define an IAP, you must input its generic identifier.

The Unity Editor and app stores use this generic identifier by default. However, you can use the __Store ID Override__ section if you need to specify a unique identifier for a specific store. 

**Export-related functions**<br/>
When you want to declare or publish a text list of IAP identifiers with an app store, you have to go to that store’s website and enter all the IAP details including the store-specific ID, title, description, price or price tier, and any localized variants to be sold in non-US regions.

For Google Play and the Apple app stores, you can use the __Google Configuration__ or __Apple Configuration__ section respectively to do this from within the Unity Editor.

The __Translations__ section provides localization functionality for Google configuration.

#### Export

After customizing your products with store-specific details, you can export the entire catalog as a .csv file to upload to Google Play, or as a text file for import through Apple’s Application Loader to the iTunes Store. 

For guidance on uploading to Google Play, see the [Google in-app billing documentation](https://developer.android.com/google/play/billing/billing_admin.html#billing-list-setup) on the [Android Developers website](https://developer.android.com). For guidance on importing through Apple’s Application Loader, see the [Application Loader documentation](https://itunesconnect.apple.com/docs/UsingApplicationLoader.pdf) on the [iTunes Connect website](https://itunesconnect.apple.com).

<a name="ExtendedFunctionality"></a>

### Accessing Unity IAP’s extended functionality

None of Unity IAP’s [extended features](UnityIAPStoreExtensions) are exposed through the Codeless IAP feature. This includes non-consumable purchase restoration for the Apple App Store (see the sample class below). 

However, through Unity’s [API scripting](ScriptingConcepts), you can edit the source for IAPButton.cs. You can access the Unity IAP [IStoreController](ScriptRef:Purchasing.IStoreController.html) and [IExtensionProvider](ScriptRef:Purchasing.IExtensionProvider.html) instances returned by [IStoreListener.OnInitialize](ScriptRef:Purchasing.IStoreListener.OnInitialized.html) to use Unity IAP’s extended functionality. Codeless IAP is an implementation on top of the existing scripting APIs, where you can augment much of Codeless IAP functionality to make it do what you want it to.

#### Apple App Store: Non-consumable purchase restoration example

The sample class below demonstrates how to access `IAppleExtensions` in order to use the purchase restoration feature:

```
using UnityEngine;
using UnityEngine.Purchasing;

public class AppleRestoreTransactions : MonoBehaviour {
	public void RestoreTransactions() {
		if (Application.platform == RuntimePlatform.OSXPlayer 
			|| Application.platform == RuntimePlatform.IPhonePlayer 
			|| Application.platform == RuntimePlatform.tvOS) {
			IAppleExtensions extensions = IAPButton.IAPButtonStoreManager.Instance.ExtensionProvider.GetExtension<IAppleExtensions>();
			extensions.RestoreTransactions(OnTransactionsRestored);
		}
	}
	private void OnTransactionsRestored(bool success) {
		Debug.Log("Transactions restored " + success.ToString());
	}
}
```