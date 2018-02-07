Getting Started
==============================


Unity supports three CPU architectures when targeting Universal Windows Platform: X86, X64 and ARM.

There are three configurations (select them in Visual Studio):

* **Debug** for debugging purposes
* **Release** for profiling
* **Master** for submission to store

The player log is located under &lt;user&gt;\AppData\Local\Packages\&lt;productname&gt;\TempState. See also [log files](LogFiles.html).

Requirements when targeting Universal Windows Platform:

* Windows 8.1
* Visual Studio 2015 (RTM or later)
* Windows 10 Universal SDK
* Testing devices:
    * For basic testing of Windows SDK 10, same PC which is used for development is enough.
    * For basic testing of Phone 10, it's advisable to acquire a real Windows Phone 10 device.

Before you can proceed you need to acquire Windows Store developer license. There are two ways you can do this: 

* Build an empty Universal Windows application from Visual Studio and deploy it, if you're doing this first time, a dialog window for getting developer license should open, follow the steps.
* See this link - [http://msdn.microsoft.com/en-us/library/windows/apps/hh974578.aspx#getting_a_developer_license_by_using_visual_studio](http://msdn.microsoft.com/en-us/library/windows/apps/hh974578.aspx#getting_a_developer_license_by_using_visual_studio)

The following are not supported:

* Legacy Network classes (please use current [Unity Networking](UNet)). WWW and UnityWebRequest are supported (applies to all scripting backends).
* `GameObject.SendMessage` partially works, but function which accepts the message must match the message sent, because the argument conversion doesn't work (applies only to .NET scripting backend).
* You cannot automatically access C# classes from JS scripts (applies only to .NET scripting backend). To do this, go to PlayerSettings (menu: __File__ > __Project Settings__ > __Player__), open the __Publishing Settings__, navigate to the __Compilation__ section and set the  __Compilation Overrides__ to __.NET Core Partially__.


###Helpful links

* Generic Universal Windows Apps samples [https://github.com/Microsoft/Windows-universal-samples](https://github.com/Microsoft/Windows-universal-samples)
* Generic forum for Universal Windows Apps [https://social.msdn.microsoft.com/Forums/windowsapps/en-us/home?forum=wpdevelop](https://social.msdn.microsoft.com/Forums/windowsapps/en-us/home?forum=wpdevelop)
* Unity forum dedicated to Windows development [http://forum.unity3d.com/forums/50-Windows-Development](http://forum.unity3d.com/forums/50-Windows-Development)

---
<span class="page-edit">• 2017-05-16  <!-- include IncludeTextAmendPageNoEdit --></span><br/>