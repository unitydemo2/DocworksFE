#CloudMoolah store 

## Sample implementation

See the sample `IAPDemo` scene and script in the default Unity IAP installation.

## Initialization

Initialization requires first configuring the `appKey` and `hashKey` using the `IMoolahConfiguration` interface.

## Configuration API

Unity IAP supports pre-initialization store-specific API through a configuration mechanism. Acquire the `IMoolahConfiguration` interface instance for CloudMoolah through the `ConfigurationBuilder.Configure<IMoolahConfiguration>()` in [Purchasing.ConfigurationBuilder.Configure](ScriptRef:Purchasing.ConfigurationBuilder.Configure.html) Scripting API.

### Secret appKey

__Syntax__

```
string IMoolahConfiguration.appKey
```

__Description__

* Required to initialize.

* Uniquely identifies the game.

* Apply for this on the Cloud Moolah Developer Portal.

* Set before Initialize is called.

__Example__

```
var builder = ConfigurationBuilder.Instance(StandardPurchasingModule.Instance());

builder.Configure<IMoolahConfiguration>().appKey = "54ad14a8a350e0a71d4764ae9825fc0e";

```

### Secret hashKey

__Syntax__

```
string IMoolahConfiguration.hashKey
```

__Description__

* Required to initialize.

* Apply for this on the Cloud Moolah Developer Portal.

* Uniquely identifies the game, and is defined by developer.

* Set before Initialize is called.

__Example__

```
var builder = ConfigurationBuilder.Instance(StandardPurchasingModule.Instance());

builder.Configure<IMoolahConfiguration>().hashKey = "asdfasdfadsfsadcok-test-a-d";

```

## Extensions API

Unity IAP supports additional store-specific API through an extension mechanism. Acquire the `IMoolahExtension` interface instance for CloudMoolah through the [IExtensionProvider](https://docs.unity3d.com/ScriptReference/Purchasing.IExtensionProvider.html) interface return by the [IStoreListener.OnInitialized](https://docs.unity3d.com/ScriptReference/Purchasing.IStoreListener.OnInitialized.html) API, for example [Unity IAP Initialization](https://docs.unity3d.com/Manual/UnityIAPInitialization.html) and [Restoring Transactions](https://docs.unity3d.com/Manual/UnityIAPRestoringTransactions.html).

### Purchasing prerequisites: registration and login 

CloudMoolah requires establishing per-user identification to create and access a user’s digital wallet. The CloudMoolah wallet collects real currency from pre-paid cards and SMS payments. Currency in the wallet is then used during the payment process. CloudMoolah requires user identification through registration and login in order to access the user's wallet. 

This identification process can be performed invisibly to the user by an application that registers and logs in using computer-generated credentials or by sharing previously created credentials from a third-party identity service. 

For example, standalone or offline games may not have access to an identity service from a game developer or publisher. In this case generating credentials may be suitable. One could register using the result of Unity’s [SystemInfo.deviceUniqueIdentifier](https://docs.unity3d.com/ScriptReference/SystemInfo-deviceUniqueIdentifier.html) API, supplying this as the user identifying "password" (__Note:__ using this API automatically adds the `android.permission.READ_PHONE_STATE` to an Android application’s manifest).

Another example is online games, which may have an online identity service available to them through their game server. In this case, copying a user-identifying credential as the registration password is appropriate.

__Note:__ The registration password must remain constant over the lifetime of the user account, serving as a permanent access token for this user’s wallet.

Purchasing requires a successful login, which requires a user to register in turn.

This Registration API is lighter in that a user only needs to provide a single password. This creates the digital wallet. Registration will also generate a "username" which is passed back to the client and must be used for the next step - login.

Login must be performed once per session. Logging in requires the generated username and user-identifying password. After the user is logged in, they may add money to the wallet through the Moo Store’s supported payment providers, and purchases can be attempted.

For users to permanently bind a wallet to an email address, they may supply additional identifying credentials such as a phone number to the Cloud Moolah web service during the purchase process on their Android device.

#### Register for a digital wallet

__Syntax__

```
void IMoolahExtension.FastRegister(string CMpassword, Action<string> registerSuccessed, Action<FastRegisterError, string> registerFailed)

```

__Parameters__

* `CMpassword`: User-defined password for signing up with the Cloud Moolah user system.

* `registerSuccessed`: Passes (string cmUserName) on successful fast registration.

* `registerFailed`: Passes error code and string description when fast registration fails.

__Description__

* Required for purchase.

* Lightweight registration with Cloud Moolah wallet. Returns a Cloud Moolah generated username. User can later perform full registration in the Cloud Moolah purchasing web service to permanently bind the wallet to the user through their phone number.

* Called after initialization.

__Example__

```

// Use custom password register a CloudMoolah acount.

m_MoolahExtensions.FastRegister("CMPassword", registerSucceed, registerFailed);

public void registerSucceed(string cmUserName)

{

    m_CloudMoolahUserName = cmUserName;

    Debug.Log ("registerSucceed : cmUserName is " + cmUserName);

}

public void registerFailed(FastRegisterError error, string errorMsg)

{

    Debug.Log ("registerFailed :FastRegisterError is " + error.ToString() + ", errorMsg is " + errorMsg);

}

```

### Log in to an existing wallet

__Syntax__

```
void IMoolahExtension.Login(string CMUserName, string CMPassword, Action<LoginResultState, string> LoginResult)
```

__Parameters__

* `CMUserName`: Returned from previous call to FastRegister (below).

* `CMpassword`: Used in previous call to FastRegister (below).

* `LoginResult`: Required. Passes (LoginResultState) attempt result along with (string message) diagnostic message.

__Description__

* Required.

* User login with Cloud Moolah username.

* All standalone games can allow users to make purchases without this login (use Unity GUID as username). 
__Example__

```
m_MoolahExtensions.Login(m_CloudMoolahUserName, "CMPassword", loginResult);

public void loginResult(LoginResultState state, string message)

{

    m_IsLoggedIn = state == LoginResultState.LoginSucceed;

}
```

## Testing

CloudMoolah supports local testing for validating an application’s purchase flow error handling, and for simulating payment without making a real-currency payment.

### Configure developer mode

__Syntax__

```
void IMoolahExtension.SetMode(CloudMoolahMode mode)
```

__Parameters__

* `mode`: Type of purchase flow to perform.

__Description__

* Supply `CloudMoolahMode` to enable success, failure, or normal operation.

__Example__

```
m_MoolahExtensions.SetMode(CloudMoolahMode.AlwaysFail); // TESTING: all purchases will fail
```

### Additional API

#### Restore previous purchase transactions

__Syntax__

```
void IMoolahExtension.RestoreTransactionID(Action<RestoreTransactionIDState> result) 
```

__Parameters__

* `result`: The status of transaction.

__Description__

* Return all unfinished transactions which have been paid for successfully but have not been paid out (see the RequestPayOut API) yet.

* Must be called after initialization.

* Must first call login.

__Example__

```
// Retrieve transaction identifiers, when Client does not already have transaction identifiers.

m_MoolahExtensions.RestoreTransactionID(( RestoreTransactionIDState restoreTransactionIDState)=>{

    // Restore complete, see ProcessPurchase for restored products

};
```

### Completely finish or consume transaction

__Syntax__

```
void IMoolahExtension.RequestPayOut(string transactionId, Action<string, RequestPayOutState, string> result)
```

__Parameters__

* `transactionId`: Transaction identifier to finish.

* `result`: TransactionId, the result of payout, any error message.

__Description__

* This is key for the delivery of a virtual item, and is helpful or necessary for offline games. This API should be used after the virtual item has been delivered.

* The use-case is that payment has been made but the games crashes before the delivery of the virtual item is complete. The standalone game developer has no record of this, so they must call the `TransactionRestore` method and the `RequestPayOut` to finish the transaction.

* For online games, developers can manage PayOut themselves, so the client does not need to call the PayOut operation and Restore. The client's game server can also do the PayOut operation by returning the delivery status while the server makes a callback.

* Call this in `ProcessPurchase`.

__Example__



For an offline game from within `ProcessPurchase`:

```

// If platform is CloudMoolah, you should to payout on a standalone game and "return PurchaseProcessingResult.Pending" at the end.

if (m_IsCloudMoolahStoreSelected) {

	m_MoolahExtensions.RequestPayOut (m_CloudMoolahTransactionID, (string transactionID, RequestPayOutState state, string message) => {

		msg = "ProcessPurchase requestPayOut TannsationID:" + transactionID + ",state:"+ state.ToString() + ",msg:" + message;

		if (state == RequestPayOutState.RequestPayOutSucceed) {

			// Finish Transaction

					m_Controller.ConfirmPendingPurchase(e.purchasedProduct);

			//payout success, issue virtual props. 

		} else {

			//PayOut Failed , Don't issue virtual props.

		}

	});

}

// You should unlock the content here.

// Indicate we have handled this purchase, we will not be informed of it again.x

// If platform is CloudMoolah,you should "return PurchaseProcessingResult.Pending" on a standalone game or "return PurchaseProcessingResult.Complete" on an online game.

return PurchaseProcessingResult.Pending;

```

For an online game:

```
// You should unlock the content here.

// Indicate we have handled this purchase, we will not be informed of it again.x

// If platform is CloudMoolah, you should "return PurchaseProcessingResult.Pending" on a standalone game or "return PurchaseProcessingResult.Complete" on an online game.

return PurchaseProcessingResult.Complete;

```

### Validate receipt on the server

__Syntax__

```
void IMoolahExtension.ValidateReceipt(string transactionId, string receipt, Action<string, ValidateReceiptState, string> result
```

__Parameters__

* `transactionId`: The payment transaction ID.

* `receipt`: Receipt data returned through ProcessPurchase.

* `result`: transactionId, enumeration of status, error message. 

__Description__

* Validate a transaction on the CloudMoolah server.

* Call after a payment.

__Example__

```
// Validate a receipt on the server.

m_MoolahExtensions.ValidateReceipt(m_CloudMoolahTransactionID, m_CloudMoolahReceipt, (string transactionID, ValidateReceiptState state, string msg)=>{

    bool succeeded = state == ValidateReceiptState.ValidateSucceed;

});
```

## Constants and enumerations

### AndroidStore - addition of CloudMoolah

__Syntax__

```
public enum AndroidStore
```

__New Member__

* `CloudMoolah`: The Cloud Moolah store’s Android identifier.

__Description__

* Indicates the Cloud Moolah store is active for Unity IAP.

* Get from the `standardPurchasingModule`’s `androidStore` field.

__Example__

```
// Determine whether we are using Cloud Moolah IAP. 

bool m_IsCloudMoolahStoreSelected = Application.platform == RuntimePlatform.Android && module.androidStore == AndroidStore.CloudMoolah;
```

### CloudMoolah store name

__Syntax__

```
string AndroidStore.CloudMoolah
```

__Description__

* The Cloud Moolah store’s shortened, readable name. 

* Constant `MoolahAppStore`.

__Example__

```
AndroidStore.CloudMoolah;
```

### Login result codes

__Syntax__

```
public enum LoginResultState

```


__Members__

* `LoginSucceed`: Successful login, session token has been generated.

* `UserNotExists`: CMUserName not found on Cloud Moolah server.

* `PasswordError`: CMPassword incorrect.

* `LoginCallBackIsNull`: Callback parameter is null.

* `UserOrPasswordEmpty`: Username or Password is empty.

* `NetworkError`: Network error.

* `NotKnown`: Unknown.

__Description__

* ICloudMoolahExtension.Login returns this state.

### FastRegistration

__Syntax__

```
public enum FastRegisterError
```

__Members__

* PasswordEmpty: CMPassword is empty.

* FastRegisterCallBackIsNull: FastRegister callback parameter is null.

* NetworkError: Network error.

* NotKnown: Unknown error.

__Description__

* Cloud Moolah Extension.FastRegister return the errors or exceptions.

* The callback will return the FastRegisterError if FastRegsiter failed.

### Receipt validation state

__Syntax__

```
public enum ValidateReceiptState
```

__Members__

* `ValidateSucceed`: Receipt validation succeeded.

* `ValidateFailed`: Receipt validation failed.

* `NotKnown`: Unknown error.

__Description__

* After purchase is done, client will query Cloud Moolah Server if the receipt is valid.

* The callback will return the result of validation.

### Transaction identifier restoration state

__Syntax__

```
public enum RestoreTransactionIDState

```

__Members__

* `NoTransactionRestor`e: No transaction needed to restore.

* `RestoreSucceed`: Restore successful.

* `RestoreFailed`: Restore failed.

* `NotKnown`: Unknown error.

__Description__

* For an offline game, the previous transactions after the login process will be restored.

* Only recommended for offline games.

* Status of return.

### Transaction completion pay out request state

__Syntax__

```
public enum RequestPayOutState
```

__Members__

* `RequestPayOutSucceed`: Payout successful.

* `RequestPayOutNetworkError`: Network error during payout.

* `RequestPayOutFailed`: Payout failed.

* `NotKnown`: Unknown error.

__Description__

* The result of calling the payout API.

* Only considered useful for offline, disconnected games - unnecessary for online, connected games.

