#PS4 Saving game data and DLC

PS4 applications save game data to various locations. These are described in detail in the [PS4 SDK documentation](https://ps4.scedev.net/resources/documents/SDK/latest/Programming-Startup_Guide/0004.html).

# Storing save data

Unity provides access to save data storage via the [PlayerPrefs](ScriptRef:PlayerPrefs.html) class, which is implemented using [PS4 Save Data memory](https://ps4.scedev.net/resources/documents/SDK/latest/SaveData-Overview/0006.html). Alternatively, you can write a native plugin that uses the PS4 **SaveData** library directly.

## PlayerPrefs

To use the `PlayerPrefs` class on PS4, you need to enable __PlayerPrefs support__ in the [PS4 Player Settings](PS4PlayerSettings). To do this, go to __Edit__ > __Project Settings__ > __Player Settings__, and select the __PS4__ tab in the Inspector window. Navigate to __Other Settings__ and check the __PlayerPrefs support__ checkbox.

You can configure the save file used by `PlayerPrefs` to set the user and file descriptions as displayed in the PS4 system settings. Use the [PS4PlayerPrefs](ScriptRef:PS4.PS4PlayerPrefs.html) class to do this. To set the icon used for the save file in the PS4 system settings, go to __Player Settings__ > __Save Data Image__, which is available when __PlayerPrefs support__ is enabled. The save file created is 10MiB. 2MiB is reserved by PS4 Save Data memory, and a total of 8MiB is available for all PlayerPref values.

[Application.Quit()](ScriptRef:Application.Quit.html) does not trigger an automatic save of `PlayerPrefs` on PS4. This is because applications cannot be directly terminated on PS4. Call [PlayerPrefs.Save](ScriptRef:PlayerPrefs.Save.html) directly to save changes to `PlayerPrefs`.

## SaveData plug-in

As with all Sony libraries, the `SaveData` API can be accessed by writing a native plug-in. You can also use Unity’s working [PS4 sample plug-in](PS4Samples), which includes source code that demonstrates use of the **SaveData** library.

## Viewing saved files

To see the files saved for your game, use the PS4 system settings menu to browse to __System Storage Management__ > __Save Data__. To see your game’s name, plus any save icon you have set, the game needs to have been installed and run as a package, rather than a PC-hosted build. Your save data will be listed for a game titled "Unknown" if there is not a package of the game installed.

# Storing downloaded data

Use the [Application](ScriptRef:Application.html) class to access the download storage area, which can be used for saving game data or files downloaded via the `WWW` class. To learn how to do this, and to learn more about how Unity maps `Application` class data paths to PS4 mount points, see documentation on [PS4 mount points](PS4ProjectStructure).

## Game data saved to download storage

Download data storage can be used to save game data, but it cannot be managed by users via PS4 system menus. Use `PlayerPrefs` or a **SaveData** plug-in to allow users to manage their game data.

## DLC saved to download storage

DLC is best handled via the [PS4DRM](ScriptRef:PS4.PS4DRM.html) class, which is built on top of Sony’s [AppContent](https://ps4.scedev.net/resources/documents/SDK/latest/AppContent-Overview/0001.html) library. To learn how to do this, see Unity’s [PS4 sample package](PS4Samples) for creating and loading DLC using `PS4DRM`. Alternatively, if you wish to host your own content, you can download it to download storage via the `WWW` class.

### WWW class on PS4

The [Caching](ScriptRef:Caching.html) class and caching functionality of [WWW.LoadFromCacheOrDownload](ScriptRef:WWW.LoadFromCacheOrDownload.html) is not implemented on PS4, so you cannot use it to store `WWW` downloads. Instead, save downloaded files using the `System.IO.File` class and manually check to see if the file exists to avoid redundant downloads.

Example:

````
string filePath = Application.persistentDataPath + "/myAssetBundle";
// Download if file doesn't exist
if (!System.IO.File.Exists(filePath))
{
    var wwwDownload = new WWW("myfiles.com/bundle1");
    yield return wwwDownload;
    System.IO.File.WriteAllBytes(fullPath, wwwDownload.bytes);
}
// Load using WWW to access Asset Bundle
var wwwFileload = new WWW("file://" + filePath);
yield return wwwFileload;
AssetBundle bundle = wwwFileload.assetBundle;
Object obj = bundle.LoadAsset("myAsset");

````

# Title User Storage (TUS)

Title User Storage (TUS) allows cloud storage of up to 64 x 64-bit integers per user, and up to 1MiB of binary data per user, for each title on the PSN servers. Additionally, 8 virtual users can be created per-title to allow common storage for all users. The Unity [NPToolKit plug-in](PS4Samples) provides an example of how to access the [Sony NpTus library](https://ps4.scedev.net/resources/documents/SDK/latest/NpTus-Overview/0001.html), including how to store `PlayerPrefs` on TUS.
