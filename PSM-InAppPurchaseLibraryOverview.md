PSM In-App Purchase Library Overview
===

## API Overview


In-App Purchase processing is implemented using the In-App Purchase library.
The In-App Purchase library retains a product list based on the contents of the metadata (app.xml).
However, data for product prices and tickets, etc. is centrally managed on a server, therefore such information must be obtained from the server in advance before purchase/consumption is performed.

![Figure 1. Processing of In-App Purchase function](../uploads/Main/inapppurchase_api_overview_1.png)

In order to obtain information from the server, use the following APIs provided by the UnityEngine.PSM.InAppPurchaseDialog in the In-App Purchase library.
In order to perform product purchasing and ticket consumption, both of the following APIs must be called in advance. (*1)

* GetProductInfo(): Gets product information
* GetTicketInfo(): Gets ticket information

Information obtained from the server will be reflected in the product list retained by the In-App Purchase library, therefore applications can obtain the latest list information using the following variable. (*2)

* ProductList: Retains product list information

In order to notify the server of purchasing/consumption based on obtained list information, use the following API. (*3)

Note that there is a possibility that a notification request entity will be processed by the server even if the result of the processing is an error. This occurs due to network disconnection after sending of a request.
Therefore, if the result of the processing is an error, use GetTicketInfo() to obtain ticket information in advance, and confirm whether purchasing and consumption have been processed by the server.

* Purchase(): Purchases the product.
* Consume(): Consumes the ticket.

## API Calls
As mentioned earlier, In-App Purchase APIs are provided to caller applications by the InAppPurchaseDialog class.
In order to obtain the results of each method in the InAppPurchaseDialog class,

* InAppPurchaseDialog.State and
* InAppPurchaseDialog.Result are used.

The execution results for methods such as GetProductInfo() and GetTicketInfo() will be stored in these variables.
In order to obtain the execution results when purchase processing, etc. has been performed, check the aforementioned variables in methods (such as Update() in the Unity script) that are called every frame.

The product information list at the time of the call will be stored in the ProductList variable in InAppPurchaseDialog.
Upon initialization, information loaded from metadata will be used in ProductList.
Since purchase processing requires the information actually registered in the server, performing each API request for GetProductInfo(), GetTicketInfo(), etc. and obtaining product information and ticket information will be required.
When calls of these APIs terminate normally, the server information will be reflected, therefore the latest product information should be obtained from these variables.

## About the Development Environment
The In-App Purchase features provide the development environment with Unity Editor and PSM DevAssistant for Unity.
An emulation feature is provided in the development environment, and the behavior differs from end user environments as listed in the following.

* It does not connect to the server.
* Purchase information is saved to a local file.
* Dialog requesting user operation is displayed every time an API is called.
* An error can be generated via the Error button or Abort button in the dialog.
* The product label string is used for the product price string.

In the development environment, dialog requesting user operation is displayed every time an API is called.

![Figure 2. Unity Editor environment dialog](../uploads/Main/InAppPurchase_Win.png)

![Figure 3. PSM DevAssistant for Unity environment dialog](../uploads/Main/InAppPurchaseSample_3.jpg)

By selecting the various buttons, it will be possible to select the server processing that occurs in In-App Purchasing.
The OK button emulates normal termination of In-App Purchase processing, and the Cancel button emulates when an end user cancels In-App Purchasing in the middle of processing.
It is also possible to press the Error button or Abort button in the dialog to confirm the behavior of the application upon a server error or communication error.

Note that in the development environment, the product label string is stored in the product price string as a precautionary measure to prevent incorrect price information.

In order to perform operation testing from the initial state, clearing the purchase information will be required. To clear purchase information in the developer environment, execute the following.

* _Unity Editor._ Select [Reset] in the emulation dialog
* _PSM DevAssistant for Unity._ Select [Reset Ticket Information] in the PSM DevAssistant for Unity menu

Since a normal type product can only be purchased once, clear the purchase information in order to perform operation testing in a state where the product does not exist after it has already been purchased.

## Error Processing

In the case when the network does not recover for a long time, if automatic retry for In-App Purchase is executed, it may become impossible to continue with the application.
Thus, it is recommended that a retry be executed according to user operation.

Moreover, when a network error occurs, the success/failure of server processing may become uncertain.
For a normal type product, information can be correctly updated as soon as the network recovers; however, for a consumable product, a comparison may be required of the states before and after the purchase processing.
Therefore, it is favorable to store the ticket state during purchase processing in save data.

The Error button emulates a state where an error occurs without the purchase or consumption processing occurring in the server.
Therefore, the local ticket file status will not change at this time. The PC simulator has an Abort button that emulates a state where an error occurs after purchase or consumption processing occurring in the server.
The local file status will change at this time, but an error will be notified

In addition, to enable use of a purchased item when a network connection cannot be established, it is recommended that the purchased item be implemented using save data.

## Notification to the User
Make notification of product information and purchase results as clear as possible to the user.

* Information regarding the product list
* Information regarding product content
* Purchased/Not purchased display for each product
* Advance notice to start purchase
* Result display when purchase succeeds
* Error display when purchase fails
