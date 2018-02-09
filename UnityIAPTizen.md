# Tizen Store

## Extended functionality

### Item Group ID

The Tizen Seller Store (also known as the Tizen Store) requires that all items available for in-app purchase be grouped into predefined Item Groups. These groups have an __Item Group ID__ assigned by the Tizen Seller Store when they are created. The ID for the group associated with your game must be passed to Unity IAP using the `SetGroupId` function:

        builder.Configure<ITizenStoreConfiguration>().SetGroupId("100000085616");

        UnityPurchasing.Initialize(this, builder);

### Store Beta vs DevMode

Unity IAP for Tizen does not use the __MODE_DEVELOPER__ option for testing. Test your in-app purchases using the Beta test functionality provided by the Tizen Seller Store.

### Purchase restoration

On startup, the Unity IAP system checks for existing Tizen purchases and processes them accordingly. During this process, your `IStoreListener.ProcessPurchase` implementation is invoked for items the user already owns. The purchase restoration process ignores consumable items.
