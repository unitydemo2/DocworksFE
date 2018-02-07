#Managed bytecode stripping with IL2CPP
Managed byte code stripping is always enabled when the [IL2CPP](IL2CPP) scripting backend is used. In this case, the Stripping Level option is replaced with an Boolean option named Strip Engine Code. If this option is enabled, unused modules and classes in the Unity Engine code will be removed. If it is disabled, all of the modules and classes in the Unity Engine code will be preserved.

The link.xml file (described below) can be used to effectively disable bytecode stripping by preserving both types and full assemblies. For example, to prevent the System assembly from being stripped, the following link.xml file can be used:

```
<linker>
       <assembly fullname="System" preserve="all"/>
</linker>
```

##Tips
###How to deal with stripping when using reflection
Stripping depends highly on static code analysis and sometimes this can’t be done effectively, especially when dynamic features like reflection are used. In such cases, it is necessary to give some hints as to which classes shouldn’t be touched. Unity supports a per-project custom stripping blacklist. Using the blacklist is a simple matter of creating a link.xml file and placing it into the Assets folder (or any subdirectory of Assets). An example of the contents of the link.xml file follows. Classes marked for preservation will not be affected by stripping:
 
```
<linker>
       <assembly fullname="System.Web.Services">
               <type fullname="System.Web.Services.Protocols.SoapTypeStubInfo" preserve="all"/>
       </assembly>

       <assembly fullname="System">
               <type fullname="System.Net.Configuration.WebRequestModuleHandler" preserve="all"/>
               <type fullname="System.Net.HttpRequestCreator" preserve="all"/>
               <type fullname="System.Net.FileWebRequestCreator" preserve="all"/>
       </assembly>

       <assembly fullname="mscorlib">
               <type fullname="System.AppDomain" preserve="fields"/>
               <type fullname="System.InvalidOperationException" preserve="fields">
                       <method signature="System.Void .ctor()"/>
               </type>
               <type fullname="System.Object" preserve="nothing">
                      <method name="Finalize"/>
               </type>
       </assembly>
</linker>
```

A project can include multiple link.xml files. Each link.xml file can specify a number of different options.
The assembly element indicates the managed assembly where the nested directives should apply.

The type element is used to indicate how a specific type should be handled. It must be a child of the assembly element. The fullname attribute can accept the ‘*’ wild card to match one or more characters.

The preserve attribute can take on one of three values:

* **all:** Keep everything from the given type (or assembly, for IL2CPP only).
* **fields:** Keep only the fields of the given type.
* **nothing:** Keep only the given type, but none of its contents.

The method element is used to indicate that a specific method should be preserved. It must be a child of the type element. The method can be specified by name or by signature.

In addition to the link.xml file, the C# `[Preserve]` attribute can be used in source code to prevent the linker from stripping that code. This attribute behaves slightly differently than corresponding entries in a link.xml file:

* **Assembly:** preserves all types in the assembly (as if a `[Preserve]` attribute were on each type)
* **Type:** preserves the type and its default constructor
* **Method:** preserves the method's declaring type, return type, and the types of all of its arguments
* **Property, Field, Event:** preserves the declaring type and return type of the property, field, or event

The stripped assemblies are output to a directory below the Temp directory in the project (the exact location varies depending on the target platform). The original, unstripped assemblies are available in the not-stripped directory in the same location as the stripped assemblies. A tool like ILSpy can be used to inspect the stripped and unstripped assemblies to determine what parts of the code were removed.

---
* <span class="page-edit">2017-09-01 <!-- include IncludeTextAmendPageSomeEdit --></span>
 
* <span class="page-history">2017-05-26 - Documentation-only update in Unity User Manual for Unity 5.6</span>
* <span class="page-history">2017-09-01 - Added advice on using C# `[Preserve]` attribute for Unity 2017.1</span>