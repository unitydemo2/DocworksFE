Getting Started
==============================


Currently if you want to build a Windows Store Apps player:

* you have to do it on Windows 8.1 or higher when targeting SDK 8.1
* you have to do it on Windows 10 or higher when targeting Universal Windows 10 Apps SDK.

Unity supports three Windows Store Apps targets:

* X86 and ARM (when targeting SDK 8.1)
* X86, X64 and ARM (when targeting Universal Windows 10 Apps)

There are three configurations (select them is Visual Studio):

* **Debug** for debugging purposes
* **Release** for profiling
* **Master** for submission to store

The player log is located under &lt;user&gt;\AppData\Local\Packages\&lt;productname&gt;\TempState. See also [log files](LogFiles.html).




###Things that are not yet supported:

* Legacy Network classes (please use current [Unity Networking](UNet)), WWW and UnityWebRequest are supported
* GameObject.SendMessage (partially works, but function which accepts the message must match the message sent, because the argument conversion doesn't work)
* You can't access C# classes from JS scripts unless you check .NET Core Partially in Compilation Overrides in PlayerSettings

###Requirements when targeting Windows SDK 8.1/Windows Phone SDK 8.1/Universal SDK 8.1:
* Windows 8.1 (**Note: Windows 8.1 N users should install this patch [http://www.microsoft.com/en-us/download/details.aspx?id=40744](http://www.microsoft.com/en-us/download/details.aspx?id=40744)**) or higher
* Visual Studio 2013 (12.021005.1 or higher)
* Testing devices:
    * For basic testing of Windows SDK 8.1, same PC which is used for development is enough.
    * For basic testing of Phone 8.1, it's advisable to acquire a real Windows Phone 8.1 device, because the emulator has a bug with touch input.

###Requirements when targeting Universal Windows 10 Apps SDK:
* Windows 8.1
* Visual Studio 2015 (RTM or later)
* Windows 10 Universal SDK
* Testing devices:
    * For basic testing of Windows SDK 10, same PC which is used for development is enough.
    * For basic testing of Phone 10, it's advisable to acquire a real Windows Phone 10 device.

###Before you can proceed you need to acquire Windows Store developer license, this can be done in two following ways:

* Build an empty Windows Store application from Visual Studio and deploy it, if you're doing this first time, a dialog window for getting developer license should open, follow the steps.
* See this link - [http://msdn.microsoft.com/en-us/library/windows/apps/hh974578.aspx#getting_a_developer_license_by_using_visual_studio](http://msdn.microsoft.com/en-us/library/windows/apps/hh974578.aspx#getting_a_developer_license_by_using_visual_studio)


###Helpful links

* Generic Windows Store Apps samples for Windows 8.1 [http://code.msdn.microsoft.com/windowsapps/Windows-8-Modern-Style-App-Samples](http://code.msdn.microsoft.com/windowsapps/Windows-8-Modern-Style-App-Samples)
* Generic Windows Universal Apps samples [https://github.com/Microsoft/Windows-universal-samples](https://github.com/Microsoft/Windows-universal-samples)
* Generic forum for Windows Store Apps [http://social.msdn.microsoft.com/Forums/windowsapps/en-US/home?category=windowsapps](http://social.msdn.microsoft.com/Forums/windowsapps/en-US/home?category=windowsapps)
* Unity forum dedicated to Windows Store Apps and Windows Phone 8 [http://forum.unity3d.com/forums/50-Windows-Development](http://forum.unity3d.com/forums/50-Windows-Development)

