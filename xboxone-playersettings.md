Xbox One Player Settings
===============


There are many player settings that are unique to the Xbox One.  Others you may be familiar with and are described on the main [Player Settings](class-PlayerSettings) page, but they are used a little differently on the Xbox One.  Most of the player settings control the values that are used in your [appmanifest.xml](xboxone-appmanifest) file.

Global Settings
---------------


![](../uploads/Main/xboxone-playersettings-globalsettings.png)  
These are settings that apply to any project you create.  You've likely already set these if you're working with an existing project.  Here are some things to keep in mind about this properties for the Xbox One.

###__Company Name__ And __Product Name__
These are used in the _appmanifest.xml_ file as the **DisplayName** and **PublisherDisplayName** respectively.  These are also used to create the AUMID and PFN for your game which are useful for [debugging](xboxone-debugging).

Per-Platform Settings -&gt; Xbox One
------------------------------------

The settings you will find in this section will effect only the Xbox One build unless otherwise noted in the UI.  In this section, you will find information about the settings that are unique to or behave differently on the Xbox One.  The settings not mentioned here are described on the main [Player Settings](class-PlayerSettings) page.

###_Icons_

![](../uploads/Main/xboxone-playersettings-icons.png)  
Here, you can set the icons that are used for your game on the Xbox One

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Override for Xbox One__|Set this property to set the icons.  If this is not set, then the default Unity logos will be used.|
|__100x100__|Shown in notification and companion center.|
|__208x208__|Shown when your game is in the recently used or pinned item section.|
|__480x480__|Shown in collections and notification center.  For DLC, this is used to identify the content within the title.|


###_Splash Images_

![](../uploads/Main/xboxone-playersettings-splash.png)  
This is the image that is used as the initial splash screen which is shown while the Xbox One Title OS is loading and during the initial loading phase of your game.  If this is not set, the splash screen will be the Unity logo on a green background.

###_Other Settings -&gt; Optimization -&gt; AOT Settings_

![](../uploads/Main/xboxone-playersettings-aotsettings.png)  
Your game scripts are compiled to native code when you build your project for Xbox One rather than at runtime.  This process is called Ahead Of Time compilation.  These are settings you can use to control how that happens.

* __AOT Compilation Options__:
    * __Debug/Development__: -debug --optimize=-linears --aot=full,asmonly,write-symbols,soft-debug,print-skipped
    * __Master__ --aot=full,asmonly,nodebug,print-skipped
* __Stripping Level__: Controls the level of bytecode stripping.  See the [Xbox One: Ahead Of Time Compiler](xboxone-aot) page for more details. (This setting is only available with the Mono scripting backend.)
* __Strip Engine Code__ Enable code stripping. (This setting is only available with the IL2CPP scripting backend.)

###_Publishing Settings_
This section holds the settings that are required to create the package for your game.  These settings correspond to data that winds up in the Unity generated [appmanifest.xml](xboxone-appmanifest) file.  The terms used are the same as used in the XDK, and you can reference the XDK documentation for more information on how these settings work.  Some of the fields here must be set with identifiers for different aspects of your game, which are identifiers you must receive from Microsoft.  There are also options to tell the Xbox One that you want to use certain features, such as the Kinect.  If you want to use these features, you must enable them in these __Publishing Settings__ as well as write the code to leverage the feature.


![](../uploads/Main/xboxone-playersettings-publishingsettings-packagetoggle.png)  

The __Content Package__ checkbox tells unity that your project should be built as a standalone game or as a content package to an existing game.  The properties in the manifest file will be different between the two.  When you have this box checked, you will be building a content package and you'll see the __Content Package__ checkbox is always visible.

####Application Manifest

![](../uploads/Main/xboxone-playersettings-appmanifest.png)  
The properties here effect the way your game and the Xbox One interact with each other. 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Content Package__|Toggle between building an game/application or a content package.|
|__App Manifest override File__|Set this to a file to use as an appxmanifest.xml file for your game or content package.  If this is set, none of the <span class="inspector">Global Settings</span>, <span class="inspector">Application Manifest</span> or <span class="inspector">Content Manifest</span> properties will effect the appxmanifest.xml, and it is your responsibility to fill out the manifest file correctly.|
|__Title ID__|A unique ID your game uses when interacting with Xbox Live Services.  You must get this ID from Microsoft.  You will not be able to use any of the Xbox Live Services if this isn't set properly.|
|__Service Config ID__|This a unique ID for accessing certain data through Xbox Live Services.  You must get this ID from Microsoft.  You will not be able to use certain aspects of the Xbox Live Services if this is not set properly.|
|__Enable GPU Variability__|Turns on notifications that you are gaining/loosing GPU resources, such as when an snapped app is opened or closed.|
|__Persistent Local Storage__|Sets the size of your game's [Persistent Local Storage](xboxone-persistentlocalstorage).|
|__Capabilities__|Features that must be explicitly marked as used if your game uses them.  See the XDK documentation for more details|
|__Supported Languages__|The languages that your game supports.  You will have to facilitate the localization of assets within your game.  See the [Manifest Localization](xboxone-manifestlocalization) page for more information.|
|__Game Age Ratings__|The rating you've been given from the various rating entities.|
|__Configured Sockets__|You must specify which sockets you will use in your game.  Clicking the <span class="menu">Add</span> or <span class="menu">Edit</span> buttons will bring up the <span class="inspector">Secure Device Socket Description</span> window.  See the [Networking](xboxone-networking) page for more information.|

####<span class="inspector">Secure Device Socket Description</span>

![](../uploads/Main/xboxone-playersettings-socketdesc.png)  
Each socket that you use on the Xbox One must be described in the manifest.  Please see the [Networking](xboxone-networking) page as well as the XDK for more information on the following properties and how networking works on the Xbox One.

|**_Property:_** |**_Function:_** |
|:---|:---|
|**Secure Device Socket Descriptions**||
|__Name__ |A name for the socket.  This is only used to identify it in the Unity Editor and in the appxmanifest.xml file.|
|__Port__ |The port number this socket will use.  The XDK lists which port numbers you may use.|
|__Protocol__|The protocol for packets sent or received with this socket.|
|__Allowed Usage__|Specifies what you will do with this socket.|
|**Secure Device Association Template**|This sets up a template that can be used for multiple connections.  Not all games will need to use this, thus these properties are optional.  Please see the XDK for more information on these properties.|
|__Template Name__|The name of the template.  This must be filled in to activate the other **Secure Device Association Template** properties.|
|__Multiplayer Requirement__|Set the multiplayer requirements for this template.  The XDK uses the term **Multiplayer Session Requirement**|
|__Allowed Usage__|Settings for what you will be doing with this template.|

####Content Manifest

![](../uploads/Main/xboxone-playersettings-contentmanifest.png)  
The <span class="inspector">Content Manifest</span> section shares the following properties with the <span class="inspector">Application Manifest</span>.  

* __App Manifest Override File__
* __Capabilities__
* __Supported Languages__

The __Allowed Products__ property is unique to the __Product ID__ and sets which games are compatible and thus allowed to load this content package.  The text field at the bottom lets you enter __Product IDs__, and you add it to the list by pressing the __Product IDs__ that you've already added will have a <span class="menu">Remove</span> button next to them that you can use to remove them from the list.

####Package Settings

![](../uploads/Main/xbxoone-playersettings-packagesettings.png)  
These settings control how your game or content package is turned into a package.  The __Build Package__ [Build Setting](xboxone-buildsettings) must be enabled to build a package.  See the [Packaging](xboxone-packaging) page and the XDK documentation for more details.


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Package Manifest Override File__ |Set this to a file to use as the manifest given to the XDK's makepkg.exe tool.  If this is set, none of the other __Launch Scene Range__ [Build Setting](xboxone-buildsettings) will have an effect.|
|__Sandbox ID__|This is an ID for a private environment for your game's data.  This is an optional setting for security purposes and is not applicable for cert as your game will be locked to the RETAIL sandbox when shipping. This is only needed if you want to ensure that your game cannot connect to any other sandbox during development.  You must use one of the existing sandboxes described in the XDK documentation or get your own, unique ID from Microsoft.|
|__Product ID__|An ID identifying your product.  This is an ID that is given to you by Microsoft.  Multiple titles can be identified as the same product.|
|__Product Description__|A description of your product.  This text is used for the *Properties > Description* section of your appxmanifest.xml file. If blank, the text will be the __Product Name__ from the global Player Settings.|
|__ContentID__|Another ID for your game and content packages.  This is an ID that is given to you by Microsoft, though a dummy ID can be used during development.|
|__Update Key__|A file used for the /updateKey option of makepkg.exe.|
|__GameOs Override__|Specify which game OS file to embed into the package.  Leave blank to use the default game OS, which is a part of the XDK installation.|
|__Package Encryption__|How to encrypt your package.  These correspond to command line options for makepkg.exe: None = /lu option, Devkit Compatible = no option, Retail Signing = /l option|
|__Update Granularity__|Corresponds to the /updcompat option for makepkg.exe.  File granularity is strongly recommended.|

####Debugging

![](../uploads/Main/xboxone-playersettings-debugging.png)  
This section has a <span class="menu">Get Log</span> button that you can use to copy the **debug.log** file for your game to your PC.  See the [Debugging](xboxone-debugging) page for details about this file.
