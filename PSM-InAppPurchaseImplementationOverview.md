PSM In-App Purchase Implementation Overview
====

## Introduction
This chapter explains how to create applications that use the In-App Purchase library based on the InAppPurchaseSample sample program.

## Creating Product Information


Use Publishing Utility for Unity to create the information (app.xml) for the product to be purchased with In-App Purchasing.
For details, refer to the manual for Publishing Utility for Unity.

## Creating an Application (Initial Processing)
Use Start() in an arbitrary Unity Script to perform the initial processing for usage of this library with the following procedure.

* In order to use the In-App Purchase feature, generate an InAppPurchaseDialog instance.

````
    void Start ()
    {
        dialog = new InAppPurchaseDialog();
    }
````

When multiple InAppPurchaseDialog instances are generated at the same time, an exception will occur.
Perform appropriate instance management by performing instance generation, etc. with the Start() method, etc. in a Unity script so that only a single instance is always generated.
In addition, make sure that In-App Purchase APIs are only called from a main thread, similar to general Unity APIs.

## Creating an Application (List Processing)

To display a product list, obtain the product information from the ProductList variable after executing the GetProductInfo() method.
In the initial state, the product price as well as the various information related to tickets will be undefined values before they are obtained from the server (determined with isTicketInfoComplete), therefore "-" will be displayed for each item in this sample.

````
    void OnGUI()
    {
        ...
        
        for (int i=0; i < dialog.ProductList.Length; i++)
        {
            var info = dialog.ProductList[i];
            
                string label = info.Label;
                string name = info.Name;
                string price = "";
                string ticket = "";
                
                InAppPurchaseTicketType type  = info.TicketType;
                
                if (dialog.IsProductInfoComplete == true)
                {
                    price = info.Price;
                }
                else
                {
                    price = "-";
                }
                
                if (dialog.IsTicketInfoComplete == true)
                {
                    if (type == InAppPurchaseTicketType.Normal)
                    {
                        ticket = info.IsTicketValid ? "YES" : "No";
                    }
                    else
                    {
                        ticket = info.ConsumableTicketCount.ToString();
                    }
                }
                else
                {
                    ticket = "-";
                }
        }
        
        ...
    }
````

## Creating an Application (Button Processing)

Implement buttons that call the ``GetProductInfo()``, ``GetTicketInfo()``, ``Purchase()``, and ``Consume()`` methods.
An exception will occur for ``Purchase()`` or ``Consume()`` if both ``GetProductInfo()`` and ``GetTicketInfo()`` have not terminated.
In this sample, the requests from the app are not arranged into any order, therefore ``Purchase()`` and ``Consume()`` can be called before ``GetTicketInfo()`` termination depending on end user operation. In such cases, catch the exception and display an error dialog. In addition, this can be dealt with by using the ``isTicketInfoComplete`` variable to check if ``GetTicketInfo()`` is already being executed or not.

````
    if (GUI.Button(rect, "GetProductInfo"))
    {
        try
        {
            dialog.GetProductInfo(GetSelectedItems());
            dialogIsBusy = true;
        }
        catch (Exception exception)
        {
            Debug.Log(exception);
        }
    }
````

## Creating an Application (Obtaining Execution Results)

Implement processing that obtain the results of the ``GetProductInfo()``, ``GetTicketInfo()``, ``Purchase()``, and ``Consume()`` methods.
Here, the current processing status is determined based on the ``InAppPurchaseDialog.State`` and ``InAppPurchaseDialog.Result`` values with the ``Update()`` method in Unity.

* If ``InAppPurchaseDialog.State`` is ``CommonDialogState.Finished`` and
* ``InAppPurchaseDialog.Result`` is ``CommonDialogState.OK``,

processing will be considered to have terminated normally.

````
    void Update ()
    {
        if (dialogIsBusy == true)
        {
            if (dialog.State == CommonDialogState.Finished)
            {
                dialogIsBusy = false;

                if (dialog.Result != CommonDialogResult.OK)
                    Debug.Log("Dialog result is \"" + dialog.Result.ToString() + "\"");

                Array.Clear(itemIsSelected, 0, itemIsSelected.Length);
            }
        }
    }
````

## After Execution (Request Complete State)

The screen when the requests in ``GetProductInfo()``, ``GetTicketInfo()``, ``Purchase()``, and ``Consume()`` complete is as follows.
For the operations of the various buttons, refer to the ``InAppPurchaseSample`` sample.

![Figure 1. State after execution](../uploads/Main/InAppPurchaseSample_2.jpg)

