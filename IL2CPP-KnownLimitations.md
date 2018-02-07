# Known limitations of IL2CPP

## Access to the MarshalAs attribute via reflection

In other .NET runtimes, you can use the [GetCustomAttributes](https://msdn.microsoft.com/en-us/library/system.attribute.getcustomattributes(v=vs.110).aspx) method to access information about the `MarshalAs` attribute that is applied to a field. IL2CPP does not support access to the attribute via reflection, which prevents Unity from storing additional metadata that would increase the final project build size.

If your project needs to reflect on data stored in a `MarshalAs` attribute, modify your game scripts to store that data in an [actual custom attribute](https://docs.microsoft.com/en-us/dotnet/standard/attributes/writing-custom-attributes), in addition to `MarshalAs`. Then you can access the data via reflection with IL2CPP.

---

* <span class="page-edit"> 2018-12-01  <!-- include IncludeTextNewPageSomeEdit --></span>