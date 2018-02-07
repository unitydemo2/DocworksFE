# Command line arguments

Unity is usually launched by double-clicking its icon from the desktop. However, it is also possible to run it from the command line (from the macOS Terminal or the Windows Command Prompt). When launched in this way, Unity can receive commands and information on startup, which can be very useful for test suites, automated builds and other production tasks.

On macOS, type the following into the Terminal to launch Unity:

````
/Applications/Unity/Unity.app/Contents/MacOS/Unity
````

On Windows, type the following into the Command Prompt to launch Unity:

````
C:\Program Files\Unity\Editor\Unity.exe
````
	 
Use the same method to launch standalone Unity games.

##Launching Unity silently

On macOS, type the following into the Terminal to silently launch Unity:

````
/Applications/Unity/Unity.app/Contents/MacOS/Unity -quit -batchmode -serial SB-XXXX-XXXX-XXXX-XXXX-XXXX -username 'JoeBloggs@example.com' -password 'MyPassw0rd'
````

**Note**: When activating via the command line using continuous integration (CI) tools like Jenkins, add the `-nographics` flag to prevent a WindowServer error.

On Windows, type the following into the Command Prompt to silently launch Unity:

````
"C:\Program Files\Unity\Editor\Unity.exe" -quit -batchmode -serial SB-XXXX-XXXX-XXXX-XXXX-XXXX -username "JoeBloggs@example.com" -password "MyPassw0rd"
````

	 
##Options

As mentioned above, the Editor and built Unity games can be supplied with additional commands and information on startup. This section describes the command line options available.

| **Command** | **Details** |
|:---|:---|
|__-assetServerUpdate &lt;IP[:port] projectName username password [r &lt;revision&gt;]&gt;__|Force an update of the project in the [Asset Server](AssetServer.html) given by `IP:port`. The port is optional, and if not given it is assumed to be the standard one (10733). It is advisable to use this command in conjunction with the `-projectPath` argument to ensure you are working with the correct project. If no project name is given, then the last project opened by Unity is used. If no project exists at the path given by `-projectPath`, then one is created automatically.|
|__-batchmode__|Run Unity in batch mode. This should always be used in conjunction with the other command line arguments, because it ensures no pop-up windows appear and eliminates the need for any human intervention. When an exception occurs during execution of the script code, the Asset server updates fail, or other operations that fail, Unity immediately exits with return code __1__. <br/>Note that in batch mode, Unity sends a minimal version of its log output to the console. However, the [Log Files](LogFiles) still contain the full log information. Opening a project in batch mode while the Editor has the same project open is not supported; only a single instance of Unity can run at a time.|
|__-buildLinux32Player &lt;pathname&gt;__|Build a 32-bit standalone Linux player (for example, `-buildLinux32Player path/to/your/build`).|
|__-buildLinux64Player &lt;pathname&gt;__|Build a 64-bit standalone Linux player (for example, `-buildLinux64Player path/to/your/build`).|
|__-buildLinuxUniversalPlayer &lt;pathname&gt;__|Build a combined 32-bit and 64-bit standalone Linux player (for example, `-buildLinuxUniversalPlayer path/to/your/build`).|
|__-buildOSXPlayer &lt;pathname&gt;__|Build a 32-bit standalone Mac OSX player (for example, `-buildOSXPlayer path/to/your/build.app`).|
|__-buildOSX64Player &lt;pathname&gt;__|Build a 64-bit standalone Mac OSX player (for example, `-buildOSX64Player path/to/your/build.app`).|
|__-buildOSXUniversalPlayer &lt;pathname&gt;__|Build a combined 32-bit and 64-bit standalone Mac OSX player (for example, `-buildOSXUniversalPlayer path/to/your/build.app`).|
|__-buildTarget &lt;name&gt;__|Allows the selection of an active build target before a project is loaded. Possible options are: <br/> standalone, Win, Win64, OSXUniversal, Linux, Linux64, LinuxUniversal, iOS, Android, Web, WebStreamed, WebGL, XboxOne, PS4, PSP2, WindowsStoreApps, Switch, WiiU, N3DS, tvOS, PSM. |
|__-buildWindowsPlayer &lt;pathname&gt;__|Build a 32-bit standalone Windows player (for example, `-buildWindowsPlayer path/to/your/build.exe`).|
|__-buildWindows64Player &lt;pathname&gt;__|Build a 64-bit standalone Windows player (for example, `-buildWindows64Player path/to/your/build.exe`).|
|__-stackTraceLogType__|Detailed debugging feature. StackTraceLogging allows features to be controlled to allow detailed logging. All settings allow __None__, __Script Only__ and __Full__ to be selected. (for example, `-stackTraceLogType Full`)|
|__-createProject &lt;pathname&gt;__|Create an empty project at the given path.|
|__-editorTestsCategories__|Filter editor tests by categories. Separate test categories with a comma.|
|__-editorTestsFilter__|Filter editor tests by names. Separate test names with a comma.|
|__-editorTestsResultFile__|Path where the result file should be placed. If the path is a folder, a default file name is used. If not specified, the results are placed in the project’s root folder.|
|__-executeMethod &lt;ClassName.MethodName&gt;__|Execute the static method as soon as Unity is started, the project is open and after the optional Asset server update has been performed. This can be used to do tasks such as continous integration, performing Unit Tests, making builds or preparing data. To return an error from the command line process, either throw an exception which causes Unity to exit with return code __1__, or call [EditorApplication.Exit](ScriptRef:EditorApplication.Exit.html) with a non-zero return code. To pass parameters, add them to the command line and retrieve them inside the function using `System.Environment.GetCommandLineArgs`. To use `-executeMethod`, you need to place the enclosing script in an Editor folder. The method to be executed must be defined as **static**.|
|__-exportPackage &lt;exportAssetPath1 exportAssetPath2 ExportAssetPath3 exportFileName&gt;__|Export a package, given a path (or set of given paths). In this example `exportAssetPath` is a folder (relative to to the Unity project root) to export from the Unity project, and `exportFileName` is the package name. Currently, this option only exports whole folders at a time. This command normally needs to be used with the `-projectPath` argument.|
|__-force-d3d11 (Windows only)__| Make the Editor use Direct3D 11 for rendering. Normally the graphics API depends on player settings (typically defaults to D3D11). |
|__-force-glcore__| Make the Editor use OpenGL 3/4 core profile for rendering. The Editor tries to use the best OpenGL version available and all OpenGL extensions exposed by the OpenGL drivers. If the platform isn't supported, Direct3D is used. |
|__-force-glcoreXY__| Similar to `-force-glcore`, but requests a specific OpenGL context version. Accepted values for XY: 32, 33, 40, 41, 42, 43, 44 or 45. |
|__-force-gles (Windows only)__| Make the Editor use OpenGL for Embedded Systems for rendering. The Editor tries to use the best OpenGL ES version available, and all OpenGL ES extensions exposed by the OpenGL drivers. |
|__-force-glesXY (Windows only)__| Similar to `-force-gles`, but requests a specific OpenGL ES context version. Accepted values for XY: 30, 31 or 32. |
|__-force-clamped__| Used with `-force-glcoreXY` to prevent checking for additional OpenGL extensions, allowing it to run between platforms with the same code paths. |
|__-force-free__| Make the Editor run as if there is a free Unity license on the machine, even if a Unity Pro license is installed.|
|__-importPackage &lt;pathname&gt;__|Import the given [package](HOWTO-exportpackage). No import dialog is shown.|
|__-logFile &lt;pathname&gt;__|Specify where the Editor or Windows/Linux/OSX standalone log file are written.|
|__-nographics__|When running in batch mode, do not initialize the graphics device at all. This makes it possible to run your automated workflows on machines that don't even have a GPU (automated workflows only work when you have a window in focus, otherwise you can't send simulated input commands). Please note that `-nographics` does not allow you to bake GI, since Enlighten requires GPU acceleration.|
|__-password &lt;password&gt;__|The password of the user, required when launching.|
|__-projectPath &lt;pathname&gt;__|Open the project at the given path.|
|__-quit__|Quit the Unity Editor after other commands have finished executing. Note that this can cause error messages to be hidden (however, they still appear in the Editor.log file).|
|__-returnlicense__|Return the currently active license to the license server. Please allow a few seconds before the license file is removed, because Unity needs to communicate with the license server.|
|__-runEditorTests__|Run Editor tests from the project. This argument requires the `projectPath`, and it's good practice to run it with `batchmode` argument. `quit` is not required, because the Editor automatically closes down after the run is finished.|
|__-serial &lt;serial&gt;__|Activate Unity with the specified serial key. It is good practice to pass the `-batchmode` and `-quit` arguments as well, in order to quit Unity when done, if using this for automated activation of Unity. Please allow a few seconds before the license file is created, because Unity needs to communicate with the license server. Make sure that license file folder exists, and has appropriate permissions before running Unity with this argument. If activation fails, see the [Editor.log](LogFiles.html) for info.|
|__-silent-crashes__|Don't display a crash dialog.|
|__-username &lt;username&gt;__|Enter a username into the log-in form during activation of the Unity Editor.|
|__-password &lt;password&gt;__|Enter a password into the log-in form during activation of the Unity Editor.|
|__-disable-assembly-updater &lt;assembly1 assembly2&gt;__ | Specify a space-separated list of assembly names as parameters for Unity to ignore on automatic updates.<br/> The space-separated list of assembly names is optional: Pass the command line options without any assembly names to ignore all assemblies, as in example 1.<br/><br/>Example 1<br/>`unity.exe -disable-assembly-updater`<br/><br/> Example 2  has two assembly names, one with a pathname. Example 2 ignores `A1.dll`, no matter what folder it is stored in, and ignores `A2.dll` only if it is stored under `subfolder` folder:<br/><br/>Example 2<br/>`unity.exe -disable-assembly-updater A1.dll subfolder/A2.dll`<br/><br/> If you list an assembly in the `-disable-assembly-updater` command line parameter (or if you don’t specify assemblies), Unity logs the following message to [Editor.log](LogFiles): <br/><br/> `[Assembly Updater] warning: Ignoring assembly [assembly_path] as requested by command line parameter.”).` <br/><br/> Use this to avoid unnecessary [API Updater](APIUpdater) overheads when importing assemblies. <br/><br/>It is useful for importing assemblies which access a Unity API when you know the Unity API doesn’t need updating. It is also useful when importing assemblies which do not access Unity APIs at all (for example, if you have built your game source code, or some of it, outside of Unity, and you want to import the resulting assemblies into your Unity project). <br/><br/> Note: If you disable the update of any assembly that does need updating, you may get errors at compile time, run time, or both, that are hard to track.|
|__-accept-apiupdate__|Use this command line option to specify that APIUpdater should run when Unity is launched  in batch mode. <br/><br/>Example:<br/><br/>`unity.exe -accept-apiupdate -batchmode [other params]`<br/><br/>Omitting this command line argument when launching Unity in batch mode results in APIUpdater not running which can lead to compiler errors. Note that in versions prior to 2017.2 there’s no way to not run APIUpdater when Unity is launched in batch mode.|

## Examples

###C#:

````
using UnityEditor;
class MyEditorScript
{
     static void PerformBuild ()
     {
         string[] scenes = { "Assets/MyScene.unity" };
         BuildPipeline.BuildPlayer(scenes, ...);
     }
}
````

###JavaScript:

````
static void PerformBuild ()
{
    string[] scenes = { "Assets/MyScene.unity" };
    BuildPipeline.BuildPlayer(scenes, ...);
}
````

The following command executes Unity in batch mode, executes the `MyEditorScript.PerformBuild` method, and then quits upon completion.

__Windows:__

````
C:\program files\Unity\Editor\Unity.exe -quit -batchmode -executeMethod MyEditorScript.PerformBuild
````

__Mac OS:__ 

````
/Applications/Unity/Unity.app/Contents/MacOS/Unity -quit -batchmode -executeMethod MyEditorScript.PerformBuild
````

The following command executes Unity in batch mode, and updates from the Asset server using the supplied project path. The method is executed after all Assets have been downloaded and imported from the Asset server. After the function has finished execution, Unity automatically quits.

```
/Applications/Unity/Unity.app/Contents/MacOS/Unity -batchmode -projectPath ~/UnityProjects/AutobuildProject -assetServerUpdate 192.168.1.1 MyGame AutobuildUser l33tpa33 -executeMethod MyEditorScript.PerformBuild -quit
```


##Unity Editor special command line arguments

These should only be used under special circumstances, or when directed by Unity Support.

| **Command** | **Details** |
|:---|:---|
|__-enableIncompatibleAssetDowngrade__|Use this when you have Assets made by a newer, incompatible version of Unity, that you want to downgrade to work with your current version of Unity. When enabled, Unity presents you with a dialog asking for confirmation of this downgrade if you attempt to open a project that would require it. <br/>**Note:** This procedure is unsupported and highly risky, and should only be used as a last resort.|


##Unity Standalone Player command line arguments

Standalone players built with Unity also understand some command line arguments:

| **Command** | **Details** |
|:---|:---|
|__-adapter N (Windows only)__|Allows the game to run full-screen on another display. The N maps to a Direct3D display adaptor. In most cases there is a one-to-one relationship between adapters and video cards. On cards that support multi-head (that is, they can drive multiple monitors from a single card) each "head" may be its own adapter. |
|__-batchmode__|Run the game in "headless" mode. The game does not display anything or accept user input. This is mostly useful for running servers for [networked games](NetworkReferenceGuide).|
|__-force-d3d11 (Windows only)__| Force the game to use Direct3D 11 for rendering. |
|__-force-d3d11-no-singlethreaded__| Force DirectX 11.0 to be created without a `D3D11_CREATE_DEVICE_SINGLETHREADED` flag.|
|__-force-glcore__| Force the Editor to use OpenGL core profile for rendering. The Editor tries to use the best OpenGL version available, and all OpenGL extensions exposed by the OpenGL drivers. If the platform isn't supported, Direct3D is used.|
|__-force-glcoreXY__| Similar to `-force-glcore`, but requests a specific OpenGL context version. Accepted values for XY: 32, 33, 40, 41, 42, 43, 44 or 45. |
|__-force-clamped__| Used together with `-force-glcoreXY`, this prevents checking for additional OpenGL extensions, allowing it to run between platforms with the same code paths. |
|__-force-wayland__| Activate experimental Wayland support when running a Linux player. |
|__-nographics__|When running in batch mode, do not initialize graphics device at all. This makes it possible to run your automated workflows on machines that don't even have a GPU.|
|__-nolog (Linux & Windows only)__|Do not produce an output log. Normally `output_log.txt` is written in the `*_Data` folder next to the game executable, where [Debug.Log](ScriptRef:Debug.Log.html) output is printed.|
|__-popupwindow__|Create the window as a a pop-up window, without a frame.|
|__-screen-fullscreen__|Override the default full-screen state. This must be 0 or 1.|
|__-screen-height__| Override the default screen height. This must be an integer from a supported resolution.|
|__-screen-width__|Override the default screen width. This must be an integer from a supported resolution.|
|__-screen-quality__| Override the default screen quality. Example usage would be: `/path/to/myGame -screen-quality Beautiful`|
|__-show-screen-selector__| Forces the screen selector dialog to be shown.|
|__-single-instance (Linux & Windows only)__|Allow only one instance of the game to run at the time. If another instance is already running then launching it again with `-single-instance` focuses the existing one.|
|__-parentHWND &lt;HWND&gt; delayed (Windows only)__|Embed the Windows Standalone application into another application. When using this, you need to pass the parent application's window handle ('HWND') to the Windows Standalone application.<br/><br/>When passing `-parentHWND 'HWND' delayed`, the Unity application is hidden while it is running. You must also call [SetParent](https://msdn.microsoft.com/en-us/library/windows/desktop/ms633541(v=vs.85).aspx) from the [Microsoft Developer library](https://msdn.microsoft.com/en-us/library/windows/) for Unity in the application. Microsoft's `SetParent` embeds the Unity window. When it creates Unity processes, the Unity window respects the position and size provided as part of the Microsoft's [STARTUPINFO](https://msdn.microsoft.com/en-us/library/windows/desktop/ms686331(v=vs.85).aspx) structure. <br/><br/> To resize the Unity window, check its [GWLP_USERDATA](https://msdn.microsoft.com/en-us/library/windows/desktop/ms633585(v=vs.85).aspx) in Microsoft's `GetWindowLongPtr` function. Its lowest bit is set to 1 when graphics have been initialized and it's safe to resize. Its  second lowest bit is set to 1 after the Unity splash screen has finished displaying.<br/>For more information, see this example: [EmbeddedWindow.zip](../uploads/Examples/EmbeddedWindow.zip)|

##Universal Windows Platform command line arguments

Universal Windows Apps don't accept command line arguments by default, so to pass them you need to call a special function from **MainPage.xaml.cs/cpp** or **MainPage.cs/cpp**. For example:

````
appCallbacks.AddCommandLineArg("-nolog");
````
	
You should call this before the `appCallbacks.Initialize()` function.


| **Command** | **Details** |
|:---|:---|
|__-nolog__| Don't produce UnityPlayer.log.|
|__-force-driver-type-warp__| Force the DirectX 11.0 driver type WARP device (see Microsoft's documentation on [Windows Advanced Rasterization Platform](http://msdn.microsoft.com/en-us/library/gg615082.aspx) for more information).|
|__-force-d3d11-no-singlethreaded__| Force DirectX 11.0 to be created without a `D3D11_CREATE_DEVICE_SINGLETHREADED` flag.|
|__-force-gfx-direct__| Force single threaded rendering.|
|__-force-feature-level-9-3__| Force DirectX 11.0 feature level 9.3.|
|__-force-feature-level-10-0__| Force DirectX 11.0 feature level 10.0.|
|__-force-feature-level-10-1__| Force DirectX 11.0 feature level 10.1.|
|__-force-feature-level-11-0__| Force DirectX 11.0 feature level 11.0.|

---
* <span class="page-edit">2017-08-07  <!-- include IncludeTextAmendPageSomeEdit --></span><br/>

* <span class="page-history">"accept-apiupdate" command line option added in Unity [2017.2](https://docs.unity3d.com/2017.2/Documentation/Manual/30_search.html?q=newin20172) <span class="search-words">NewIn20172</span></span>

* <span class="page-history">"-force-clamped" command line argument added in Unity [2017.3](https://docs.unity3d.com/2017.3/Documentation/Manual/30_search.html?q=newin20173) <span class="search-words">NewIn20172</span></span>

* <span class="page-history">Tizen support discontinued in [2017.3](https://docs.unity3d.com/2017.3/Documentation/Manual/30_search.html?q=newin20173) <span class="search-words">NewIn20173</span></span>
