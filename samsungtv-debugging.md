#Samsung TV Debugging

## Obtaining Debug.Log output in realtime

Logs can be accessed in realtime while the game is running via a telnet connection to Unity Launcher.

**OSX:**

 1. Launch Terminal.app and type:
> _telnet &lt;tv ip address&gt; 2333_

 1. You should see **Welcome To Unity Launcher** message.  You will now get logs from Unity games in this window.

**Windows:**

 1. Download [puttytel.exe](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) and launch it.
 1. Insert TV's IP Address and check **Telnet**.  Input port **2333**.
![](../uploads/Main/samsungtv-telnet1.png)
 1. Click **Terminal**, check **Implicit CR for every LF**, then click **Open**.
![](../uploads/Main/samsungtv-telnet2.png)
 1. You should see **Welcome To Unity Launcher** message.  You will now get logs from Unity games in this window.
![](../uploads/Main/samsungtv-telnet3.png)

## Manually uploading / launching / uninstalling games

Unity Launcher contains a web interface for managing your development games.  You can also obtain logs from current / previous runs here.

![](../uploads/Main/samsungtv-unitylauncher.png)

You can access this page by navigating to **http://&lt;tv ip&gt;:8899** in your web browser.

### Unity Launcher Game List
A list of all games you currently have installed.  The following options are available for each game:

| | |
|:---|:---|
| **Launch** | Starts the game on the TV |
| **Uninstall** | Removes the game from the USB drive |
| **Log** | Displays the log from the last run |
| **Prev Log** | Displays the log from the run before the last |

### Unity Launcher Global Actions

| | |
|:---|:---|
| **Storage Location** | If you have multiple USB drives in your TV, you can switch between them here |
| **Get Full Log** | Gets the full log for _all_ games since Unity Launcher started |
| **Get Prev Full Log** | Gets the full log for the last run of Unity Launcher.  Useful if your application crashed to see what went wrong. |
| **Exit Unity launcher** | Quits Unity Launcher |

### Game Archive Upload

Zip files are produced when Unity exports to the Samsung TV target.  These files can be uploaded to the TV via Unity Launcher web interface in this section.  Click **Choose File** and select the zip file that was exported.  Make sure you select the correct year (2013 vs. 2014 vs. 2015), and click **Upload**.  Check the Full Log or realtime log if the game does not show up.

#### Samsung TV Packages

When you build in Unity for the Samsung TV Platform, you will get one zip file for each model year.  Ex:

* MyGame_STANDARD_13.zip
* MyGame_STANDARD_14.zip
* MyGame_STANDARD_15.zip
* MyGame_STANDARD_16.zip

The correct zip will be automatically uploaded to your TV and launched when _Build And Run_ is clicked.  If you need to upload manually, be sure to select the correct year for your TV.

## Debugging Crash Issues

If your game crashes and returns the the App Selection Screen:

 1. Relaunch Unity Launcher and navigate to the web interface at **http://&lt;tv ip&gt;:8899**.  Click **Get Prev Full Log** and inspect the log for any error messages.
 1. It is possible that you ran out of graphics memory.  Try reducing texture sizes.
 1. Review [crash checklist](MobileCrashes).
 1. Review [mobile developer checklist](MobileDeveloperChecklist).
