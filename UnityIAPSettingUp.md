#Setting up Unity IAP

Once you have [set up your project for Unity Services](SettingUpProjectServices), you can enable the Unit IAP service.

## Step 1. Enable In-App Purchasing

In the __Services window__, select __In-App Purchasing__.

![](../uploads/Main/UnityIAPOff.png)

Click the __Enable__ button to enable In-App Purchasing.

![](../uploads/Main/UnityIAPEnable.png)

### Note: Common Unity IAP integration compiler errors
The following error messages may indicate that Unity IAP is disabled in the Unity Cloud Services window, or that Unity is disconnected from the Internet: 

* CS0246: The type or namespace name IPurchaseReceipt could not be found.
* System.Reflection.ReflectionTypeLoadException
* UnityPurchasing/Bin/Stores.dll
* UnityEngine.Purchasing

To resolve these errors, first try reloading the Services window. A quick way to do this is to close it and then reopen it. Once reloaded, make sure that Unity IAP is enabled.

If this doesn’t work, try disconnecting and reconnecting to the Internet, then sign back into Unity Services and re-enable Unity IAP. Only users with Unity Services "owner" or "manager" roles for the registered organisation can enable the Unity IAP Service. 

## Step 2. COPPA Compliance

The Children's Online Privacy Protection Act (COPPA) applies to the online collection of personal information from children under 13. The rules spell out what you must include in a privacy policy, when and how to seek verifiable consent from a parent, and what responsibilities you have to protect children's privacy and safety online. If you have not already specified a COPPA choice in your Analytics settings, a dialog window will appear asking about the target age for users of your app in order to ensure COPPA compliance. Choose the appropriate answer and then click __Save Changes__.

![The COPPA Compliance target age prompt](../uploads/Main/UnityIAPCoppa.png)

## Step 3. Adding the IAP package

To import the Unity IAP package into your project, click __Import__.

![The IAP Import Package option](../uploads/Main/UnityIAPImportPackage.png)

When you import the package, a new folder called __Plugins__ is automatically added to your project. This folder contains UnityPurchasing assets required to use Unity IAP.

![The imported IAP package files in the project window](../uploads/Main/UnityIAPImportedPackage.png)

Click __Back to services__ to review the Services panel.

![The Services window back button](../uploads/Main/UnityServicesBack.png)

Make sure that that Analytics and In-App Purchasing are both labelled __ON__ as shown below.

![Services window showing IAP and Analytics switched on](../uploads/Main/UnityServicesIAPandAnalyticsOn.png)

You can now begin implementing Unity In-App Purchases into your project.
