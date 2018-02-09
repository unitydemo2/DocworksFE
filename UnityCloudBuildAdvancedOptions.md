# Advanced options

Once you’ve configured your project in Unity Cloud Build, you can set up advanced build options for each of your build targets. 

These options are designed to accommodate the more complex build processing options supported in the Unity Editor.

To access your build target’s advanced options, go to the [Unity Developer website](http://developer.cloud.unity3d.com). Select your project, enter the __Unity Cloud Build__ section for the project, then select the __Config__ tab, shown below. 

![](../uploads/Main/UnityCloudBuildAdvancedOptions-Config.png)

Click  __[+]  Show Advanced Options__, shown below. This displays a drop-down list of the build target’s __Advanced Options__.

![](../uploads/Main/UnityCloudBuildAdvancedOptions-AdvancedOptions.png)
The title changes to __[-] Hide Advanced Options__ when the __Advanced Options__ drop-down is expanded.

![](../uploads/Main/UnityCloudBuildAdvancedOptions-AdvancedOptionsExpanded.png)

Click __Edit Advanced Options__ to bring up a screen to configure these options.

![The Edit Advanced Options screen](../uploads/Main/UnityCloudBuildAdvancedOptions-AdvancedOptionsEdit.png)

##Advanced options per build target

All advanced options are set per build target. This means that, for example, when you click the __Advanced Options__ link for an iOS target, those options are only for that iOS target. When you click __Advanced Options__ for an Android target, those options are only for that Android target. This allows you to use different pre- and post-methods per platform, per build target.

![](../uploads/Main/UnityCloudBuildAdvancedOptions-PerTarget.png)

##Making development builds

A development build includes debug symbols and enables the Profiler. 

See documentation on [Development builds](UnityCloudBuildDevelopmentBuilds) for more information.

##Pre- and post-export methods

Sometimes you need to manipulate the project files before or after the project is built in Unity. Examples include copying variables from an external file into the project, processing Assets, or working with plug-ins that require special treatment. 

See documentation on [Pre- and post-export methods](UnityCloudBuildPreAndPostExportMethods) for more information.

##Using Xcode frameworks

When building for iOS, you might need to include various frameworks after the Unity build process is done, but before the Xcode build process starts. 

See documentation on [Xcode frameworks](UnityCloudBuildXcodeFrameworks) for more information. 

##Custom scripting #define directives

Unity includes a feature named **Platform Dependent Compilation**. This consists of preprocessor directives that let you partition your scripts to compile and execute a section of code exclusively for one of the supported platforms. You can also specify your own #define directives for each build target. 

See documentation on [Custom scripting #define directives](UnityCloudBuildCustomScriptingDefineDirectives) for more information.

##Custom Scene list

Use this if you want to configure a build target to build a set of Scenes that’s different to what is set up in the project’s **Build Settings** menu in the Unity Editor.

See documentation on [Including specific Scenes](UnityCloudBuildIncludingSpecificScenes) for more information.