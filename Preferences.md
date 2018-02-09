#Preferences

Unity provides a number of preference settings to allow you to customise the behaviour of the Unity Editor. To access them, go to __Unity__ > __Preferences__ (on macOS) or __Edit__ > __Preferences...__ (Windows).

##General

![](../uploads/Main/PrefsGeneral.png) 

| __Setting__ | __Properties__ |
|:---|:---|
|__Auto Refresh__|Check this box to update Assets automatically as they change.|
|__Load Previous Project on Startup__|Check this box to always load the previous project at startup.|
|__Compress Assets on Import__|Check this box to automatically compress Assets during import.|
|__OSX Color Picker__ (macOS)| Check this box to use the native macOS color picker instead of Unity's own.|
|__Disable Editor Analytics__ (Pro only)|Check this box to stop the Editor automatically sending information back to Unity.|
|__Show Asset Store search hits__ |Check this box to show the number of free/paid Assets from the Asset Store in the Project Browser. |
|__Verify Saving Assets__|Check this box if you wish to verify which Assets to save individually on quitting Unity.|
|__Editor Skin__ (Plus/Pro only)|Select the drop-down to choose which skin to apply to the Unity Editor. Choose __Personal__ for light grey with black text, or __Professional__ for dark grey with white text.|
|__Enable Alpha Numeric Sorting __|Check this box to enable a new button in the top-right corner of the [Hierarchy](Hierarchy) window, allowing you to switch between Transform sort (which is the default behaviour) and Alphanumeric sort.|


##External tools

![](../uploads/Main/PrefsExtTools.png) 


| __Setting__ | __Properties__ |
|:---|:---|
|__External Script Editor__|Select which application Unity should use to open script files. Unity automatically passes the correct arguments to script editors it has built-in support for. Unity has built-in support for MonoDevelop, Xamarin Studio, Visual Studio (Express) and Visual Studio Code.|
|__External Script Editor Args__|Select which arguments to pass to the external script editor.<br/>`$(File)` is replaced with a path to a file being opened.<br/>`$(Line)` is replaced with a line number that editor should jump to.<br/>`$(ProjectPath)` is replaced with the path to the open project.<br/> If not set on macOS, then the default mechanism for opening files is used. Otherwise, the external script editor is only launched with the arguments without trying to open the script file using the default mechanism. <br/> See below for examples of external script editor arguments.|
|__Add .unityproj's to .sln__|Check this box to add UnityScript (.unityproj) projects to the generated solution (.sln) file. This is enabled by default for MonoDevelop and Xamarin Studio, and disabled by default for Visual Studio (Express) and Visual Studio Code.|
|__Editor Attaching__|Check this box to allow debugging of scripts in the Unity Editor. If this option is disabled, it is not possible to attach a script debugger to Unity to debug your scripts.|
|__Image application__|Choose which application you want Unity to use to open image files.|
|__Revision Control Diff/Merge__|Choose which application you want Unity to use to resolve file differences with the Asset server. Unity detects these tools in their default installation locations (and checks registry keys for TortoiseMerge, WinMerge, PlasticSCM Merge, and Beyond Compare 4 on Windows). |

###Examples of script editor arguments

* **Gvim/Vim**: `--remote-tab-silent +$(Line) "$File"`
* **Notepad2**: `-g $(Line) "$(File)"`
* **Sublime Text 2**: `"$(File)":$(Line)`
* **Notepad++**: `-n$(Line) "$(File)"`




##Colors

![](../uploads/Main/PrefsColors.png) 

This panel allows you to choose the colors that Unity uses when displaying various user interface elements.


##Keys

![](../uploads/Main/PrefsKeys.png) 

This panel allows you to set the keystrokes that activate the various commands in Unity.



##GI Cache 

![](../uploads/Main/PrefsGICache.png) 


| __Setting__ | __Properties__ |
|:---|:---|
|__Maximum Cache Size (GB)__| Use the slider to set the maximum GI cache folder size. The GI cache folder will be kept below this size whenever possible. Unused files are periodically deleted to create more space. This is carried out by the Editor automatically, and doesn't require you to do anything.|
|__Custom cache location__|Check this box to allow a custom location for the GI cache folder. The cache folder will be shared between all projects.|
|__Cache compression__|Check this box to enable a fast real-time compression of the GI Cache files, to reduce the size of the generated data. If you need to access the raw Enlighten data, disable Cache Compression and clean the cache.|
|__Clean Cache__| Use this button to clear the cache directory.|

##2D


![](../uploads/Main/Prefs2D.png)

| __Setting__ | __Properties__ |
|:---|:---|
|__Maximum Sprite Atlas Cache Size (GB)__|Use the slider to set the maximum sprite atlas cache folder size. The sprite atlas cache folder will be kept below this size whenever possible.|



##Cache Server

![](../uploads/Main/PrefsCacheServer.png) 


| __Setting__ | __Properties__ |
|:---|:---|
|__Use Cache Server__|Check this box to use a dedicated cache server.|
|__IP Address__|Enter the IP address of the dedicated cache server here, if enabled.|
