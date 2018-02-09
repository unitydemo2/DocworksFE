# Xcode frameworks

If your iOS project requires additional Xcode frameworks, use the [PBXProject](ScriptRef:iOS.Xcode.PBXProject-ctor.html) API to add those frameworks to the Xcode project files created by Unity Cloud Build.

There are two ways to call this API to manipulate the Xcode project:

* Use the built-in Unity [PostProcessBuildAttribute](ScriptRef:Callbacks.PostProcessBuildAttribute.html), which is executed before the Unity Cloud Build Post-Export method runs.

* Use the [Unity Cloud Build post-export method](UnityCloudBuildPreAndPostExportMethods).

**Note**: if you are using a version of Unity earlier than 5.0, add this functionality to your Unity project using the [Xcode Manipulation API](https://bitbucket.org/Unity-Technologies/xcodeapi) provided by Unity on [Bitbucket](https://bitbucket.org/Unity-Technologies/xcodeapi).