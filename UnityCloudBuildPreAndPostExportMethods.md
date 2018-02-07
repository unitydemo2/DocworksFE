# Pre- and post-export methods

Once you’ve created a build target in Unity Cloud Build, you can set pre- and post-export methods in that build target’s __Advanced Options__.  (See documentation on accessing and editing [Advanced Options](UnityCloudBuildAdvancedOptions).)



![The Edit Advanced Options screen](../uploads/Main/UnityCloudBuildAdvancedOptions-AdvancedOptionsEdit.png)

Specify the __Pre-Export Method Name__ and the __Post-Export Method Name__ here.

The pre- and post-export methods allow you to trigger actions before and after your Unity project is built. These methods must exist as code within your project in the __Editor__ folder in your __Asset__ folder.

##Pre-Export Method Name

If you create a public static method in your Unity project, you can direct Unity Cloud Build to execute it before the project is exported by the Unity Editor. When Unity Cloud Build calls this method it passes a `BuildManifestObject` as an optional parameter. For example: `Namespace.NeatMethod(UnityEngine.CloudBuild.BuildManifestObject)`, where `BuildManifestObject` is the build manifest for the current build. See [Build manifest](UnityCloudBuildManifest) for more information.

##Post-Export Method name

If you create a public static method in your Unity project, you can direct Unity Cloud Build to execute it after the project is exported by the Unity Editor. When Unity Cloud Build calls this method it passes a string as a parameter. For example: `Namespace.OtherMethod(string)`, where `string` is the path to the exported project. In the case of iOS, your project can then know the location of the Xcode project before it is processed by Xcode and turned into the iOS application .ipa file.

**Note**: If you've tagged any methods in your code with the Unity [PostProcessBuildAttribute](ScriptRef:Callbacks.PostProcessBuildAttribute.html), those methods are executed before any methods configured as post-export methods in Unity Cloud Build.
