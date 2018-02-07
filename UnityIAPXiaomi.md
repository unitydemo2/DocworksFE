#Unity IAP Xiaomi integration guide

##Overview
[Unity IAP](https://docs.unity3d.com/Manual/UnityIAP.html) provides a streamlined channel for developers outside of China to publish apps in the Chinese market. This guide introduces the Unity Channel SDK, and describes the end-to-end process for a developer publishing IAP content to the [Xiaomi Mi Game Center](http://app.mi.com/) platform.

Publishing a game to the Mi Game Center is a 3-step process:

1. Submit your Xiaomi-configured game package through [Unity Cloud Build](https://docs.unity3d.com/Manual/UnityCloudBuild.html).
2. In the [Xiaomi-Unity developer portal](https://developer.unity.mi.com/), populate your game’s store metadata.
3. Release your game upon Xiaomi approval.

###Xiaomi Mi Game Center
The Mi Game Center is Xiaomi’s official Android store. It allows users to search, browse and purchase products for the Xiaomi platform using a secure payment portal. For more information, visit [Unity’s Xiaomi partner site](https://unity3d.com/partners/xiaomi).

###Unity Channel
[Unity Channel](https://docs.unity3d.com/Manual/UnityIAPXiaomiAPI.html) is an internal component of Unity IAP that helps developers outside of China access the Chinese app store market by facilitating user login, payment management, and Chinese Government app distribution regulatory approval.

Because of Unity Channel, Xiaomi Mi Pay integration differs from Google Play and iTunes in the following ways:

* Xiaomi games require a [Unity IAP Catalog](#ProductCatalog). Google Play and iTunes support entirely backend-defined Products. However, the Xiaomi client SDK built into Unity IAP depends on the Product IDs and metadata being available on the client.
* Codeless IAP support is planned but not yet available (check forums for updates).
* During Unity IAP initialization, Product ownership information is not returned to the client. Therefore, developers must track user purchases through their servers or locally on the device.

###Requirements
* The Unity Channel SDK is designed for use with Unity versions 2017.1+, however it is backwards compatible with versions 5.3+.
* The Unity Channel SDK is included in [Unity IAP](https://assetstore.unity.com/packages/add-ons/services/billing/unity-iap-68207) versions 1.13.0+.
* Xiaomi IAP support is only available for Android builds. The appropriate [Android and Java SDKs](#AndroidConfigure) are required.
* Pushing builds to Xiaomi requires the [Unity Cloud Build](https://docs.unity3d.com/Manual/UnityCloudBuild.html) service.
* Xiaomi does not currently support [Codeless IAP](https://docs.unity3d.com/Manual/UnityIAPCodelessIAP.html) implementation.

##Building your Project for Xiaomi
This section describes the process of configuring your game through the Unity Editor using the Unity IAP SDK:

* Setting up your Project
* Adding the Xiaomi package to your Project
* Enabling IAP
* Creating an IAP Catalog

###Setting up your Project
<a name="AndroidConfigure"></a>
####Configuring for Android
Xiaomi only supports Android builds. Configuring your Project for Android is a 4-step process.

1. Download and install the [Android](https://developer.android.com/studio/index.html) and [Java](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) SDKs. For more information, see documentation on [Getting started with Android Development](https://docs.unity3d.com/Manual/android-GettingStarted.html).
2. Set the SDK file path targets. In the Unity Editor, select __Edit__ > __Preferences__, then select __External Tools__ from the left navigation bar. Scroll down to the __Android__ section, and set the __SDK__ and __JDK__ fields to reflect the file paths where you installed the Android and Java SDKs respectively (see image 1.1, below; note that you can select the __Download__ buttons next to each field for direct links to each SDK’s download webpage).
3. Set the application’s Package Name. Xiaomi requires the application’s __Package Name__ to follow the “BuildName.mi” convention. Select __Edit__ > __Project Settings__ > __Player__ to open the Player Settings window. Then select the Android tab (see image below) and, under __Other Settings__ > __Identification__, and set the __Package Name__ field (see image 1.2, below). 
4. Build the Project for Android. In the Editor, select __File__ > __Build Settings__, then select __Android__ from the menu. Select __Build__ to test that Unity can locate the SDKs and compile your build.

![Image 1.1: Specifying file locations to the Android and Java SDKs in the Unity Editor.](../uploads/Main/SDKSettings.png)

![Image 1.2: Setting your app’s package name in the Unity Editor Android settings.](../uploads/Main/PackageNameSettings.png)

<a name="UnityChannelInstall"></a>
####Adding the Xiaomi Asset package to your Project
In the Editor, enable Unity IAP from the Services window (__Window__ > __Services__; see documentation on [Setting up Unity IAP](https://docs.unity3d.com/Manual/UnityIAPSettingUp.html)). Be sure to Import the IAP Asset package when prompted (see image below). As of version 1.13.0, the Unity IAP Asset package includes the Unity Channel and Xiaomi SDKs.

![Enabling Unity IAP and importing the Xiaomi SDK via the Unity Editor’s Services window.](../uploads/Main/EnablingIAP.png)

####[Optional] Standalone SDK
If you wish to publish your app to the Mi Game Center without in-app purchasing, install the Xiaomi Unity Channel standalone SDK from the Build Settings window (__File__ > __Build Settings__) by selecting __Android__ from the __Platform__ menu and selecting __Add__ from the __Xiaomi Game Center__ menu option that appears.

![Installing the Unity Channel standalone SDK from the Build Settings window.](../uploads/Main/StandaloneSDK.png)

<a name="AppStoreSettings"></a>
###App store settings
Unity Channel includes an Asset that provides an Editor interface for managing app store credentials and test mode functionality. This __AppStoreSettings__ Asset installs to _Assets/Plugins/UnityChannel/XiaomiSupport/Resources_ when you import the Unity IAP Asset package. You can also create it manually in the Editor by selecting __Assets__ > __Create__ > __App Store Settings__. Access the interface by selecting the Asset and viewing the Inspector.

![The AppStoreSettings asset provides a GUI for managing your app’s credentials.](../uploads/Main/AppStoreSettings.png)

**Note**: The __AppStoreSettings__ Asset is only available in Unity 5.6+.

In order to communicate, the Unity and Xiaomi servers both require unique identifiers for your game. Note that you can retrieve your Unity Client credentials [here](https://id.unity.com/en/user_clients/settings) by pasting your Project ID into the search field. Unity 5.3 or 5.4 users must retrieve and set credentials this way, as they cannot access the __AppStoreSettings__ Asset. The settings depicted in the image above are described below:

1. The __Generate Unity Client__ button populates Unity credentials that bind to your Project. <br/><br/> **Note**: Generating, loading, or updating Unity client credentials sends networked requests to Unity’s backend server. Progress for this operation appears in the Console log.<br/><br/>
2. __Client ID__ and __Client Key__ are required to communicate through Unity IAP to the Unity Channel and Xiaomi backends. The Unity Channel backend proxies receipt validation requests (for more information, see documentation on [Unity IAP receipt validation](https://docs.unity3d.com/Manual/UnityIAPValidatingReceipts.html), and the __Receipt validation and extensions__ section of  the [Unity Channel SDK](https://docs.unity3d.com/Manual/UnityIAPXiaomiAPI.html) documentation).
3. __Client RSA Public Key__ is an optional security layer. Use it to receive server callbacks for client-side receipt validation, or to integrate with Unity server APIs. <br/><br/> **Note**: __Client Secret__ is another optional security layer should you wish to implement server-side validation. __Client Secret__ is auto-generated with the other credentials. Refresh it any time by selecting __Update Client Secret__ from the __AssetStoreSettings__ Asset.<br/><br/>
4. Provide an optional __Callback URL__ for your game server to receive purchase transaction data.
5. Xiaomi distributes __App ID__, __App Key__, and __App Secret__ credentials during the submission process. You must save them to your App Store Settings before submitting your final build for publication.
6. __Test Mode__ is required for [testing your application’s purchase flows](#TestingIntegration) and [submitting to Xiaomi](#XiaomiSubmission). 

You need these credentials and the test mode toggle at various points of the integration process. Note that App Store Settings data updates server-side, as opposed to saving to your client.

##Implementing IAP
###Enabling the Unity IAP service
If you enabled Unity IAP to [import the Xiaomi Asset package](#UnityChannelInstall), no action is required. Otherwise, see documentation on [Setting up Unity IAP](https://docs.unity3d.com/Manual/UnityIAPSettingUp.html) to enable the service.

You can also install the latest Unity IAP plugin through the [Unity Asset Store](https://www.assetstore.unity3d.com/en/#!/content/68207). 

<a name="ProductCatalog"></a>
###Creating a Product Catalog
The Xiaomi client SDK built into Unity IAP depends on Product metadata being available in the client. As such, you must define your Products through the Editor’s IAP Catalog GUI (__Window__ > __Unity IAP__ > __IAP Catalog__). 


![The IAP Catalog window provides a GUI for building and exporting your app’s Product catalog.](../uploads/Main/IAPCatalogGUI.png)


Populating the Catalog
The IAP Catalog GUI defines Products along with their metadata for the game client’s runtime. Documentation on [Codeless IAP](https://docs.unity3d.com/Manual/UnityIAPCodelessIAP.html) contains information on configuring Products through the IAP Catalog. The following Product attributes warrant attention for Xiaomi specifically:

![Breakdown of the IAP Catalog editor.](../uploads/Main/CatalogEditor.png)

1. __ID__ is a unique identifier (string data type) required by the Mi Game Center.
2. __Type__ indicates the durability of the Product. Xiaomi supports consumable and non-consumable Product Types. It does not support subscription Product Types.
3. The __Descriptions__ section controls __Title__ and __Description__ text for use on the Mi Store. You must specify __Simplified Chinese__ from the __Locale__ drop-down menu (this is currently the only supported language).
4. __Pay Configuration__ controls the Product’s price point. The Unity Channel SDK supports predefined Chinese yuan pricing tiers for Xiaomi, but not arbitrary values.

For more information about Product attributes and their parameters, see documentation on [Defining Products](https://docs.unity3d.com/Manual/UnityIAPDefiningProducts.html). 

<a name="ExportCatalog"></a>
####Exporting the Catalog for Xiaomi’s developer portal
In the Editor, in the IAP Catalog window, export the Catalog by selecting __App Store Export__ > __Xiaomi Mi Pay Catalog__. 

![Exporting your app’s Product catalog for the Xiaomi developer portal.](../uploads/Main/ExportCatalog.png)

Export the _MiGameProductCatalog.prop_ file to your location of choice. Import your Product catalog on the [Xiaomi developer portal](https://developer.unity.mi.com/) by navigating to your Project’s __IAP Configuration__ tab and selecting __Import__ (see section on [Importing your IAP Product catalog](#ImportCatalog), below).  


![Example of the Xiaomi developer portal reading the _MiGameProductCatalog.prop_ file for its interface.](../uploads/Main/ImportCatalog.png)

Exporting the IAP Catalog also writes a copy of the _MiGameProductCatalog.prop_ file to your Project’s _Assets/Plugins/Android/assets/_ directory (see image below). Unity IAP uses this file in the IAP Catalog editor and at runtime. It also serves as a default Product catalog for your app if no catalog file is explicitly imported through the Xiaomi developer portal.

![The Product catalog exported.](../uploads/Main/PropFile.png)

<a name="Initialization"></a>
###Client-side initialization
Unity IAP typically requires a configuration builder that consumes IAP Catalog data to be parsed for the destination store, followed by the Unity IAP ```Initialize()``` API (see documentation on [Initializing IAP](https://docs.unity3d.com/Manual/UnityIAPInitialization.html)).

Xiaomi games require an extra step prior to initializing IAP, because the Mi Game Center requires apps to share their credentials through the [login API](https://docs.unity3d.com/Manual/UnityIAPXiaomiAPI.html) at launch.

The modified initialization process becomes:

1. Initialize the Unity Channel Xiaomi API.
2. Log in to the Unity Channel Xiaomi API.
3. Initialize Unity IAP as normal by running a configuration builder instance, then call the Unity IAP ```initialize()``` API.

Execute these steps early in the game’s runtime lifecycle, preferably at launch. You can implement them in the same script.

####1. Xiaomi Login 
The following example illustrates how to modify initialization using the Unity Channel SDK to call the login API:

```
using AppStoreSupport;
using System;
using System.Collections;
using UnityEngine;
using UnityEngine.Purchasing;
using UnityEngine.Store;

// Run the script once, at game launch.
public class UnityChannelSample : MonoBehaviour
{
	// Xiaomi login requires a login listener.
	// Create one by implementing the ILoginListener abstract class included in the Unity Channel SDK.
	class SampleLoginListener : ILoginListener
	{
		public Action initializeIAP;

		// Step 1 succeeded; call step 2
		public void OnInitialized()
		{
			Debug.Log("Initialization succeeded.");
			UnityEngine.Store.StoreService.Login(this); // If initialization succeeds, initiate Xiaomi login
		}

		// Step 1 failed; display error message and recourses
		public void OnInitializeFailed(string message)
		{
			Debug.Log("Initialization failed.");
		}

		// Step 2 completed; call step 3
		public void OnLogin(UserInfo userInfo)
		{
			Debug.Log(string.Format("Login successful: userId {0}, userLoginToken {1}, channel {2}", userInfo.userId, userInfo.userLoginToken, userInfo.channel));
			// When login succeeds, proceed to initializing IAP
initializeIAP(); 
		}

		// Step 2 failed; display error message and recourses
		public void OnLoginFailed(string message)
		{
			Debug.Log("Login failed.");
		}
	}
}
```

**Note**: You must use all of the functions in the above sample code, which account for all possible steps of the login process. However, you can choose the actions called within each function. In this example, debug text appears in place of action calls. In this example, the OnLogin() method initiates a Unity IAP initialization function.   

####2. Xiaomi initialization
Next, initialize the Xiaomi API using a login listener and the app credentials stored in your __AppStoreSettings__ Asset:

```
	void Awake()
	{
		// Create a login listener based on the SamleLoginListener class
		SampleLoginListener loginListener = new SampleLoginListener();

		// Tie the initializeIAP Action (from the SampleLoginListener class) to a function (defined in the next step)
		loginListener.initializeIAP = ConfigureIAP;

		// Access the AppStoreSettings Asset to generate AppInfo with your stored credentials. The AppStoreSettings class is part of the AppStoreSupport library. 
		AppStoreSettings appStoreSettings = Resources.Load<AppStoreSettings>("AppStoreSettings");

		// Initialize Xiaomi using the credentials and login listener
		UnityEngine.Store.StoreService.Initialize(appStoreSettings.getAppInfo(), loginListener);
	}
```

Upon loading your Project’s __AppStoreSettings__ Asset, the ```getAppInfo()``` function returns credential data for the Mi Game Center store initialization process.

####3. Unity IAP configuration builder and initialization
Finally, use a configuration builder to translate Product data from your IAP Catalog for Xiaomi, then [initialize Unity IAP](https://docs.unity3d.com/2017.2/Documentation/Manual/UnityIAPInitialization.html):

```
	// The configuration builder requires a store listener. 
	// Create one by implementing the IStoreListener abstract class.
	class StoreListener : IStoreListener
	{
		private IStoreController controller;
		private IExtensionProvider extensions;

		// Called when Unity IAP is ready to make purchases.
		public void OnInitialized(IStoreController controller, IExtensionProvider extensions)
		{
			this.controller = controller;
			this.extensions = extensions;
		}

		// Note that this will not be called if Internet is unavailable;
		// Unity IAP will attempt initialization until it becomes available.
		public void OnInitializeFailed(InitializationFailureReason error)
		{
		}

		// Called when a purchase completes, or Unity IAP encounters an unrecoverable initialization error;
		// may be called at any time after OnInitialized().
		public PurchaseProcessingResult ProcessPurchase(PurchaseEventArgs e)
		{
			return PurchaseProcessingResult.Complete;
		}

		// Called when a purchase fails.
		public void OnPurchaseFailed(Product i, PurchaseFailureReason p)
		{
		}
	}

	// Run a configuration builder to define your Products
	public void ConfigureIAP()
	{
		// Load Products from the IAP Catalog
		var module = StandardPurchasingModule.Instance();
		var builder = ConfigurationBuilder.Instance(module);
		var catalog = ProductCatalog.LoadDefaultCatalog();

		// Loop through Products in Catalog, extracting metadata to the builder
		foreach (var product in catalog.allProducts)
		{
			if (product.allStoreIDs.Count > 0)
			{
				var ids = new IDs();
				foreach (var storeID in product.allStoreIDs)
				{
					ids.Add(storeID.id, storeID.store);
				}
				builder.AddProduct(product.id, product.type, ids);
			}
			else
			{
				builder.AddProduct(product.id, product.type);
			}
		}

		// Create a store listener based on the StoreListener class
		StoreListener storeListener = new StoreListener();

		// Initialize Unity IAP
		UnityPurchasing.Initialize(storeListener, builder);
	}
```

The configuration builder references Product IDs and Product Types to automate population of Price, Type, Title, and Description metadata. It uses your IAP Catalog’s _IAPProductCatalog.json_ file and the ```builder``` object instantiated during Unity IAP initialization.

###Implementing IAP purchasing
For information on methods for in-game purchase implementation, see documentation on the following:

* [Codeless IAP](https://docs.unity3d.com/Manual/UnityIAPCodelessIAP.html)
* [Unity IAP Initialization](https://docs.unity3d.com/Manual/UnityIAPInitialization.html)
* [Unity Channel SDK](https://docs.unity3d.com/Manual/UnityIAPXiaomiAPI.html)

<a name="TestingIntegration"></a>
###Testing integration
Test your game’s purchase flows on a non-Xiaomi Android device by toggling test mode in the [__AppStoreSettings__ Asset interface](#AppStoreSettings). Unity Channel also provides an API for toggling test mode:

```AppInfo.debug = true;``` 

The Unity Channel wrapper includes the ```AppInfo``` class, and passes data to the Xiaomi SDK. To submit your app to Xiaomi, you must enable test mode. Test mode also bypasses the credit card requirement for testing purposes. After enabling test mode, build your Project and launch the resulting APK file from an Android device.

To test real purchasing, set test mode to false and test on a Xiaomi device. Please note that real purchasing requires a [Xiaomi Mi Pay Account](https://account.xiaomi.com) and appropriate currency such as Chinese Yuan.

<a name="XiaomiSubmission"></a>
##Submitting to Xiaomi
This section describes the process of submitting your game through the Unity Editor using the Unity IAP SDK:

1. Set the IAP target
2. Test IAP integration
3. Register the application
4. Push your game to the Xiaomi portal

###Setting the IAP target
In the Unity Editor, set Unity IAP to target Mi Game Pay by selecting __Window__ > __Unity IAP__ > __Android__ > __Target Xiaomi Mi Game Pay__. This enables Xiaomi for the next build of the game’s APK. It also creates the configuration file that informs Unity IAP at runtime to use the Xiaomi Mi Pay native billing API.

![Setting Unity IAP to target Xiaomi Mi Game Pay during the next construction of your app’s build.](../uploads/Main/TargetXiaomi.png)

###Pushing the Project to the Xiaomi developer portal
Before pushing to Xiaomi, test building your game, either locally or by configuring the Project with an Android build target in Unity Cloud Build (see documentation on [Cloud Build](https://docs.unity3d.com/Manual/UnityCloudBuild.html)).

In the Editor, enable Cloud Build through the Unity Services window (see documentation on [Cloud Build implementation](https://developer.cloud.unity3d.com/support/)). 

####Upload the build 
Upload your build to the build history for your project, using one of two methods:

**From the Editor**: 

1. In the Cloud Build Services window, select __Manage Target Builds__ > __Add New Target__.
2. In the __TARGET SETUP__ menu, set the __PLATFORM__ field to __Android__ and enter a useful __TARGET LABEL__. Then select __Next: Save__.
3. Select __Start Cloud Build__, then select the target build you just created. 


![Uploading a Cloud Build via the Editor.](../uploads/Main/CloudUpload.png)

**From the [Unity Cloud Build Developer Dashboard](https://developer.cloud.unity3d.com/build):**

1. Navigate to your Project’s __Cloud Build History__.
2. Select __Upload__, then select the APK file you built from the Editor.

![Uploading a Cloud Build via the Developer Dashboard.](../uploads/Main/DashUpload.png)

####Push the build to Xiaomi
Push the the hosted build to Xiaomi’s developer portal, using one of two methods: 

**From the Editor:** 

In the Cloud Build Services window, locate the desired build from the build history timeline and select __Push to Xiaomi__. Verify that you want to push, and that the action completes.

![Pushing a hosted build to Xiaomi’s developer portal via the Editor.](../uploads/Main/EditorPush.png)

**From the [Unity Cloud Build Developer Dashboard](https://developer.cloud.unity3d.com/build):**

1. Navigate to your Project’s __Cloud Build History__. 
2. Select __Download .APK__ file, then select __Push to Xiaomi__ from the dropdown menu.

![Pushing a hosted build to Xiaomi’s developer portal via the Unity Developer Dashboard.](../uploads/Main/DashPush.png)

###Configuring the game in the Xiaomi developer portal
Your UDN credentials grant access to your uploaded Projects in the [Xiaomi Unity developer portal](https://developer.unity.mi.com/). The first time you log in, you must acknowledge Xiaomi’s Terms and Conditions before proceeding to your __Projects__ list. Locate the Project you wish to submit. Its status (highlighted below) will initially read __Version1.0: Draft__. Select the clipboard icon to view a submission log of your Project’s status changes throughout the process. Select the status link to expand your Project’s metadata details.

![Your Projects list in the Xiaomi developer portal.](../uploads/Main/XiaomiProjects.png)

The following details are illustrated in the image below:

![A Project’s store metadata expanded in the Xiaomi developer portal.](../uploads/Main/XiaomiProjectDetails.png)

####1. Basic Information
This section contains the text to display on the Mi Game Center.

* __Game Name__ is the English title of your app. Xiaomi will manually translate the English title to Chinese for the customer-facing storefront.
* __Name of Developer__ is your customer-facing publisher name.
* __Game Introduction__ is the English description of your app. Note that Xiaomi will manually translate the English title to Chinese for the customer-facing storefront.
* __Email__ is the developer contact information Xiaomi should use to initiate feedback.

####2. Target Device
This section contains marketing assets for Phone and Tablet devices that display on the Mi Game Center. Note the following guidelines: 

* You must upload a minimum of 3 images for each device type that you check.
* Image dimensions must either be 1080 x 720 pixels (landscape), or 720 x 1080 pixels (portrait).

###Submitting for review
When you are ready, select __Submit__ to submit your game to Xiaomi for review. The status indicator for your Project changes to __In review__. While your Project is in review, you cannot edit its details. Expand the Project and select __Cancel__ to cancel the review and revise the Project’s details.

####Regional compliance with regulations
You need an ISBN publication license to publish your app. Xiaomi provides comprehensive support for the ISBN approval process through the State Administration of Press, Publication, Radio, Film and Television (SAPPRFT).


Xiaomi does not guarantee that the SAPPRFT will approve all games (see [SAPPRFT submission guidelines](http://www.miit.gov.cn/n1146290/n4388791/c4638978/content.html)). To meet store and country compliance rules, you may need to make some changes to your game. 

####Content guidelines for a smooth approval process
Consider the following tips when submitting for Chinese government approval: 

* Avoid depicting Chinese national landmarks and symbolism (for example, the Chinese national flag, or the Great Wall) in a manner that could be considered undignified. 
* Avoid depicting Chinese national politics, history, conflicts, or religions entirely. 
* When creating maps and regions in your game’s world, avoid defining regions that conflict with China’s existing geopolitics and borders. 
* Avoid depiction of gambling, and gambling mechanics of any kind.
* China has tight restrictions on mature content. Avoid depictions of nudity, realistic violence, and drug usage.
* Avoid depicting minors participating in any illegal activities, such as underage drinking and smoking.

<a name="ImportCatalog"></a>
####Importing your IAP Product catalog
Before finalizing your submission, follow these steps to ensure Xiaomi has your most current IAP Product catalog:

1. Select your Project, then select __IAP Configuration__ from the left navigation bar.
2. Select __Import__.
3. Import the _MiGameProductCatalog.prop_ file you [exported from your Project](#ExportCatalog).
4. Verify the contents of the catalog, then select __Confirm__.
5. A list of your imported Products appears. Select __Submit__ to save the catalog to your submission.

![Importing an IAP catalog to the Xiaomi developer portal.](../uploads/Main/XiaomiCatalogImport.png)

##Publishing to the Mi Game Center
###Credentials
When Xiaomi indicates approval, your project status changes to __Approved__ and receives the following credentials: 

* __App ID__
* __App Key__
* __App Secret__

![An approved Project on the Xiaomi developer portal.](../uploads/Main/ApprovedProject.png)

Enter these credential values in the [__AppStoreSettings__ Asset](#AppStoreSettings) or [initialization script](#Initialization), then set [test mode](#AppStoreSettings) to ```false```. Create a new build of your game, and push this build to Xiaomi as before.

Xiaomi provides a developer contract via email. Once you sign the contract, Xiaomi facilitates the government approval process. It will notify you when the game receives an ISBN license and clearance to publish on the Mi Game Center. 

Xiaomi’s content review process typically takes 1-2 business days, unless it recommends changes. The government approval process and license distribution, however, can take 4-8 months. For more information on the review process, please see the **FAQs** section of the [Unity-Xiaomi partner page](https://unity3d.com/partners/xiaomi).

