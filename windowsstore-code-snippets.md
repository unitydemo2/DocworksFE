Windows Store Apps: Code snippets
========================


####How to to implement "Rate Us" functionality?

Associate these lines with button click.

````
#if NETFX_CORE
			string productID =  Windows.ApplicationModel.Package.Current.Id.FamilyName;
			Application.OpenURL("ms-windows-store://pdp/?ProductId=" + productID);
#endif
````