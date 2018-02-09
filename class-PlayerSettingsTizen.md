#Tizen Player Settings

This page details the __Player Settings__ specific to Tizen. A description of the general Player Settings can be found [here](class-PlayerSettings).


##Resolution And Presentation

![](../uploads/Main/PlayerSetTizenResPres.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|**Resolution** ||
|__Default Orientation__ |(This setting is shared between iOS, Android and Tizen devices)|
|__Default Orientation__ |The game's screen orientation. The options are **Portrait** (home button at the bottom), **Portrait Upside Down** (home button at the top), **Landscape Left** (home button on the right side), **Landscape Right** (home button on the left side) and **Auto Rotation** (screen orientation changes with device orientation).|
|__Use Animated Autorotation__ |Should orientation changes animate the screen rotation rather than just switch? (Only visible when the _Default Orientation_ is set to _Auto Rotation_.)|
|**Allowed Orientations for Auto Rotation** |(Only visible when the _Default Orientation_ is set to _Auto Rotation_.)|
|__Portrait__ |Allow portrait orientation. |
|__Portrait Upside Down__ |Allow portrait upside down orientation.|
|__Landscape Right__ |Allow landscape right orientation (ie, home button on the **left** side). |
|__Landscape Left__ |Allow landscape left orientation (home button is on the **right** side).|
|__Disable Depth and Stencil__ |Should the depth and stencil buffers be disabled? |


##Icon

![](../uploads/Main/PlayerSetTizenIcon.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Override for Tizen__ |Check if you want to assign a custom icon you would like to be used for your Tizen game.|


##Other Settings

![](../uploads/Main/PlayerSetTizenOther.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|**Rendering** ||
|__Rendering Path__ |The [rendering path](RenderingPaths) enabled for the game. |
|__Static Batching__ |Set this to use Static batching on your build (enabled by default). |
|__Dynamic Batching__ |Set this to use Dynamic Batching on your build (enabled by default). |
|**Identification** ||
|__Bundle Identifier__ |The string used in your provisioning certificate from your Samsung Tizen Store account(This is shared between iOS, Android and Tizen) |
|__Bundle Version__ |Specifies the build version number of the bundle, which identifies an iteration (released or unreleased) of the bundle. The version is specified in the common format of a string containing numbers separated by dots (eg, 4.3.2). |
|**Configuration** |
|__Disable HW statistics__|Disables the application from sending hardware statistics to Unity (see the  [hwstats](http://hwstats.unity3d.com/) page for details).|
|__Scripting Define Symbols__|Custom compilation flags (see the [platform dependent compilation](PlatformDependentCompilation) page for details).|
|**Optimization** ||
|__Api Compatibility Level__ |Specifies active .NET API profile. See below|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__.Net 2.0__ |.Net 2.0 libraries. Maximum .net compatibility, biggest file sizes|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__.Net 2.0 Subset__ |Subset of full .net compatibility, smaller file sizes|
|__Prebake Collision Meshes__|Should collision data be added to meshes at build time? |
|__Preload Shaders__|Should shaders be loaded when the player starts up? |
|__Preloaded Assets__|An array of assets to be loaded when the player starts up. |
|__Stripping Level__ |Options to strip out scripting features to reduce built player size(This setting is shared between iOS and Android Platforms)|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Disabled__ |No reduction is done.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Strip Assemblies__ |Level 1 size reduction.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Strip ByteCode__ |Level 2 size reduction (includes reductions from Level 1).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Use micro mscorlib__ |Level 3 size reduction (includes reductions from Levels 1 and 2).|
|__Vertex Compression__|Select whic vertex channels should be compressed. Compression can save memory and bandwidth but precision will be lower.|
|__Optimize Mesh Data__|Remove any data from meshes that is not required by the material applied to them (tangents, normals, colors, UV).|

##Publishing

![](../uploads/Main/PlayerSetTizenPub.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Product Description__ |A description of your application that is stored in the manifest and used in the Tizen Store. |
|__Product URL__ |The URL for your application that is stored in the manifest and used in the Tizen Store. If you do not have a website for your application you may leave this blank. |
|__Signing Profile Name__ |Set this to the name of the signing profile that you have set up in the Tizen IDE. (Window > Preferences > Tizen SDK > Security Profiles > Profiles). If you have not given your profile a name then use the word "default" (without quotes). |
|__Capabilities__ |Select any additional application capabilities that you may need. For example: Location service or any capabilities that are required for native plugins that have been included in your project. |

###API Compatibility Level

You can choose your mono api compatibility level for all targets. Sometimes a 3rd party .net dll will use things that are outside of the .net compatibility level that you would like to use. In order to understand what is going on in such cases, and how to best fix it, get "Reflector" on windows. 

1. Drag the .net assemblies for the api compatilibity level in question into reflector. You can find these in Frameworks/Mono/lib/mono/YOURSUBSET/
1. Also drag in your 3rd party assembly.
1. Right click your 3rd party assembly, and select "Analyze".
1. In the analysis report, inspect the "Depends on" section. Anything that the 3rd party assembly depends on, but is not available in the .net compatibility level of your choice will be highlighted in red there.


##Details


###Bundle Identifier

The __Bundle Identifier__ string must match the provisioning profile of the game you are building. The basic structure of the identifier is __com.CompanyName.GameName__. This structure may vary internationally based on where you live, so always default to the string you set in the Tizen Seller Store.

###Stripping Level

Most games don't use all necessary dlls. With this option, you can strip out unused parts to reduce the size of the built player on Tizen devices. If your game is using classes that would normally be stripped out by the option you currently have selected, you'll be presented with a Debug message when you make a build.
