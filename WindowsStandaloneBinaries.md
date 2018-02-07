#Windows standalone Player build binaries
When you build a Unity project to the Windows standalone platform Unity produces the following files (where 'ProjectName' is the name of your project):

* `ProjectName.exe` - The project executable. This contains the program entry point which calls into the Unity engine when launched.

* `UnityPlayer.dll` - this DLL contains all the native Unity engine code. It is also signed using the Unity Technologies certificate, allowing easy verification that the engine was not tampered with.

* `*.pdb files` - Symbol files for debugging. Unity copies these to the build directory if you enable __Copy PDB files__ in the Build Settings window.

* `WinPixEventRuntime.dll` - This DLL enables [Windows PIX profiler](https://blogs.msdn.microsoft.com/pix/2017/01/17/introducing-pix-on-windows-beta/) support. Unity only creates this file if you check the __Development Build__ checkbox in the Build Settings window. 

* `ProjectName_Data folder` - This folder contains all the data needed to run your project.

##Rebuilding the game executable
Unity creates the source code for `ProjectName.exe` in this  folder: *Editor\Data\PlaybackEngines\WindowsStandaloneSupport\Source\WindowsPlayer*.

To modify the executable, or ship code which you built yourself (if you want to sign it, for example), you must rebuild the executable and place it in your built game directory. 

To build your executable outside of Unity, you need [Visual Studio](https://www.visualstudio.com/) 2015 or 2017 with 'Common Tools for Visual C++'' and 'Windows XP support for C++' installed.

---
* <span class="page-edit">2017-07-19  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Windows standalone Player build binaries changed in [2017.2](https://docs.unity3d.com/2017.2/Documentation/Manual/30_search.html?q=newin20172) <span class="search-words">NewIn20172</span></span>

