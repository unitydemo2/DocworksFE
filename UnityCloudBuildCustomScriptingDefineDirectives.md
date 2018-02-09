# Custom scripting #define directives

Using Unity Cloud Build, you can create  custom scripting #define directives.
On the [Unity Developer website](https://developer.cloud.unity3d.com), go to the build target’s __Advanced Options__. (See documentation on accessing and editing [Advanced Options](UnityCloudBuildAdvancedOptions).)



![The Edit Advanced Options screen](../uploads/Main/UnityCloudBuildAdvancedOptions-AdvancedOptionsEdit.png)

In the __Scripting Define Symbols__ field, you can add your own custom scripting #define directives to the the built-in selection available. For each build target, enter the names of the symbols you want to define. You can then use these symbols as the conditions in #if directives, just like the built-in ones. 

For more information, see documentation on [Platform-dependent compilation](PlatformDependentCompilation).