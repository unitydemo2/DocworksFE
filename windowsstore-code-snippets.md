Universal Windows Platform: Code snippets
========================


####How to to implement "Rate Us" functionality?

Associate these lines with button click.

````
#if ENABLE_WINMD_SUPPORT
			string productID =  Windows.ApplicationModel.Package.Current.Id.FamilyName;
			Application.OpenURL("ms-windows-store://pdp/?ProductId=" + productID);
#endif
````

---
<span class="page-edit">• 2017-05-16  <!-- include IncludeTextAmendPageNoEdit --></span><br/>