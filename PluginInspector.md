#Plugin Inspector

The Plugin Inspector is used to select and manage target platforms for the plugins in your project. Simply select a plugin file to view its Inspector.

![Inspector for a plugin called "CustomConnection"](../uploads/Main/PluginInspector.png)

Under __Select platforms for plugin__, choose which platforms will use the plugin by checking the appropriate boxes. If you select __Any Platform__, the plugin will apply to all platforms, including the Unity editor. 

Once you have selected the platforms, you can choose additional options such as CPU type and specific OS from the separate __Platform Settings__ section below. This contains a tab for each platform selected by the checkboxes. Most platforms have no settings, or just a few (such as CPU and OS selection).

The current list of file extensions that are treated as plugins and display the Plugin Inspector in the Unity Editor is found in `PluginImporter::CanLoadPathNameFile()`. The following file extensions identify files that are treated as plugins:

* .dll
* .winmd
* .so 
* .jar
* .aar
* .xex
* .def
* .suprx
* .prx
* .sprx
* .rpl
* .cpp
* .cc 
* .c
* .h
* .jslib
* .jspre
* .bc 
* .a
* .m
* .mm 
* .swift
* .xib

Certain folders are treated as a single bundle plugin. No additional plugins are detected within such folders. The following extensions identify folders that are treated as bundle plugins: 

* .framework
* .bundle
* .plugin


## Default settings
To make transition easier from earlier Unity versions, Unity will try to set default plugins settings, depending on the folder where the plugin is located.


| **Folder** | **Default settings** |
|:---|:---|
|**Assets/\../Editor**| Plugin will be set only compatible with Editor, and won't be used when building to platform.|
|**Assets/\../Editor/**(**x86** or **x86_64** or **x64**)| Plugin will be set only compatible with Editor, CPU value will be assigned depending on the subfolder.|
|**Assets/\../Plugins/**(**x86_64** or **x64**)| x64 Standalone plugins will be set as compatible.|
|**Assets/\../Plugins/x86**| x86 Standalone plugins will be set as compatible.|
|**Assets/Plugins/Android/**(**x86** or **armeabi** or **armeabi-v7a**)| Plugin will be set only compatible with Android, if CPU subfolder is present, CPU value will be set as well.|
|**Assets/Plugins/iOS**| Plugin will be set only compatible with iOS.|
|**Assets/Plugins/WSA/**(**x86** or **ARM**) | Plugin will be set only compatible with Universal Windows Platform, if subfolder is CPU present, CPU value will be set as well. Metro keyword can be used instead of WSA.|
|**Assets/Plugins/WSA/**(**SDK80** or **SDK81** or **PhoneSDK81**)| Same as above, additionally SDK value will be set, you can also add CPU subfolder afterwards. For compatibility reasons, SDK81 - Win81, PhoneSDK81 - WindowsPhone81.|
|**Assets/Plugins/Tizen**| Plugin will be set only compatible with Tizen.|
|**Assets/Plugins/PSVita**| Plugin will be set only compatible with Playstation Vita.|
|**Assets/Plugins/PS4**| Plugin will be set only compatible with Playstation 4.|

## Device-specific settings

####Editor settings

![Options in the editor tab](../uploads/Main/PluginInspectorEditorTab.png)

For instance, if you select **CPU X86**, the plugin will be used only in **32 bit Editor**, but will not be used in **64 bit Editor**.

If you select **OS Windows**, the plugin will be used only in **Windows Editor**, but will not be used by the **OS X Editor**.

#### Standalone settings
See [Standalone player settings](class-PlayerSettingsStandalone).

#### Universal Windows Platform
See:

* [Universal Windows Platform: Plugins on .NET Scripting Backend](windowsstore-plugins.html "Plugins")

* [Universal Windows Platform: Plugins on IL2CPP Scripting Backend](windowsstore-plugins-il2cpp.html "Plugins")

#### Android
When building for Android, folders found with a parent path matching exactly __Assets/Plugins/Android/__ are treated as an Android Library plugin folder. They are then treated in the same way as folders with the special extensions .plugin, .bundle and .framework.

#### iOS

![iOS plugin settings, showing Framework dependencies](../uploads/Main/PluginiOSExample.png)

---

* <span class="page-edit">2017-11-20  <!-- include IncludeTextAmendPageNoEdit --></span><br/>

* <span class="page-history">Removed Samsung TV support.</span>

