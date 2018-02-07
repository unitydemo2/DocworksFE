#Log Files


There might be times during development when you need to obtain information from the logs of the standalone player you've built, the target device, or the Editor. Usually you need to see these files when you have experienced a problem, to find out exactly where the problem occurred.

On macOS, the player and Editor logs can be accessed uniformly through the standard __Console.app__ utility.

On Windows, the Editor logs are placed in folders which are not shown in the Windows Explorer by default. See below.

##Editor

To view the Editor log, select __Open Editor Log__ in Unity's Console window.

|OS |Log files |
|:---|:---|
|**macOS** | `~/Library/Logs/Unity/Editor.log`|
|**Windows XP** | `C:\Documents and Settings\username\Local Settings\Application Data\Unity\Editor\Editor.log`|
|**Windows Vista/7** | `C:\Users\username\AppData\Local\Unity\Editor\Editor.log`|

On macOS, all the logs can be accessed uniformly through the standard __Console.app__ utility.

On Windows, the Editor log file is stored in the local application data folder &lt;LOCALAPPDATA&gt;\Unity\Editor\Editor.log, where &lt;LOCALAPPDATA&gt; is defined by [CSIDL_LOCAL_APPDATA](https://msdn.microsoft.com/en-us/library/windows/desktop/bb762494%28v=vs.85%29.aspx).

##Player

|OS |Log files |
|:---|:---|
| **macOS** | `~/Library/Logs/Unity/Player.log` |
|**Windows XP** | `C:\Documents and Settings\username\Local Settings\Application Data\CompanyName\ProductName\output_log.txt`|
|**Windows Vista/7** | `C:\Users\username\AppData\LocalLow\CompanyName\ProductName\output_log.txt`|
| **Linux** | `~/.config/unity3d/CompanyName/ProductName/Player.log` |

Note that on Windows and Linux standalones, the location of the log file can be changed (or logging suppressed). See documenttion on [Command line arguments](CommandLineArguments) for further details.

###iOS
Access the device log in XCode via the GDB console or the Organizer Console. The latter is useful for getting crashlogs when your application was not running through the XCode debugger.

The [Troubleshooting](TroubleShootingIPhone) and [Reporting crash bugs](iphone-bugreporting) guides may be useful for you.

###Android
Access the device log using the [logcat console](http://developer.android.com/guide/developing/tools/adb.html#logcat). Use the __adb__ application found in __Android SDK/platform-tools directory__ with a trailing __logcat__ parameter:

`$ adb logcat`

Another way to inspect the LogCat is to use the [Dalvik Debug Monitor Server (DDMS)](http://developer.android.com/guide/developing/debugging/ddms.html). DDMS can be started either from __Eclipse__ or from inside the __Android SDK/tools__. DDMS also provides a number of other debug related tools.

### Universal Windows Platform

|Device |Log files |
|:---|:---|
|**Desktop** |`%USERPROFILE%\AppData\Local\Packages<productname>\TempState\UnityPlayer.log`|
|**Windows Phone**| Can be retrieved with [Windows Phone Power Tools](https://wptools.codeplex.com/). The [Windows Phone IsoStoreSpy](https://isostorespy.codeplex.com/) can also be helpful. |

###WebGL

On WebGL, log output is written to the browser's [JavaScript console](webgl-debugging).

##Accessing log files on Windows

On Windows, the log files are stored in locations that are hidden by default. In Windows XP, make hidden folders visible in Windows Explorer using __Tools__ > __Folder Options...__ > __View (tab)__.

On Windows Vista/7, make the AppData folder visible in Windows Explorer using  __Tools__ > __Folder Options...__ > __View (tab)__. The Tools menu is hidden by default; press the Alt key once to display it.

---
* <span class="page-edit">• 2017-05-16  <!-- include IncludeTextAmendPageNoEdit --></span><br/>

* <span class="page-history">Tizen support discontinued in [2017.3](https://docs.unity3d.com/2017.3/Documentation/Manual/30_search.html?q=newin20173) <span class="search-words">NewIn20173</span></span>

