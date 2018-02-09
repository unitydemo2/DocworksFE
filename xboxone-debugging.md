Debugging
=========


There are some things that you will need to keep in mind when debugging on the Xbox One compared to other platforms.  For master builds, all debugging capabilities except native debugging through Visual Studio are turned off.

Player Log File
---------------

Log statements from your script and from Unity will be printed to a file called **debug.log** to the root folder of your game on the devkit.  This can be an important tool when debugging problems within your game.  You can retrieve the log file with tools like the XDK's _Xbox One Manager_ or *copy* from the command line.  All the text in the log file is also passed to the OutputDebugString function, so it will show up in the stream monitored by the XDK's _xbdbgmon_ tool or Visual Studio if it's connected to the process.

The root folder for your game is the same as its PFN.  When your game is deployed to the kit, it is given two identifiers: an AUMID and a PFN.  These are used by the XDK tools to access your game's files, including the player log file, on the Xbox One console.  The XDK documentation will have more information on what these identifiers are, how they're used, and how to find them.  One of the quicker ways of getting it is by using the XDK's _xbapp list_ command.  This will give you a list of PFNs with their AUMIDs indented underneath.  Both will contain your company and game name, but without spaces or underscores.

You can have the log file created on the consoles development or temporary drive by adding the **-logtodev** or **-logtotemp** command line options when launching your game.  This will be necessary when you need the log from a package build because your game's root folder is read-only when built as a package.  Keep in mind that the development drive is shared, so your log file can be overwritten if you launch another game or app.

Please see the XDK documentation section *Xbox One XDK &gt; Developement Environment &gt; Overviews &gt; Xbox One Neighborhood: Accessing the Console File System from Your PC* for more details on how to access files on the console.


Script Debugging With Mono Develop
----------------------------------

Script debugging works the same as on other platforms: enable "Script Debugging" for your Unity build and use the *Run > Attach to Process...* command in Mono Develop.  It may take a few seconds for the IP to show up in Mono Develop's "Attach to Process" window.

In order for Mono to connect to the console, it must be on the same subnet as the development PC that is running Mono Develop.  The console uses broadcast messages on ports 4600 and 4601 to communicate with the debugger, and Mono listens to these messages using port 34997.  Your network or firewalls (including any software firewalls on your development machine such as Windows Firewall) must allow communication using the ports and broadcast messages (make sure to exempt both the UnityEditor and MonoDevelop's executables).  
 

Native Debugging
----------------

If a native crash occurs, a crash dump file will be created for you.  This file can be opened in Visual Studio or sent to Unity to help diagnose the crash.  You will find the file on the development drive of your kit, and you can retrieve it with tools like the XDK's _Xbox One Manager_ or *copy* from the command line.  Please see the XDK documentation section *Xbox One XDK &gt; Developement Environment &gt; Overviews &gt; Xbox One Neighborhood: Accessing the Console File System from Your PC* for more details on how to access files on the console.

Native symbols for all build types are available and can be found in the sub directories of the *&lt;unity install path&gt;\Data\PlaybackEngines\XboxOnePlayer\Varitions* directory.  The development build type uses the release executables and symbols.

Different parts of the Unity Engine run on separate threads, including some of the functionality from Unity's Xbox One Plugins.  Because of this, you may find yourself wanting to find out what other threads are doing at a particular moment of time when you're debugging.  It is important to remember that Unity's main loop does not run on your game's main thread.  The Xbox One OS controls the main thread, and starts up Unity's main loop on a worker thread.  From your game's point of view however, this worker thread is considered the main thread for all intents and purposes.  To differentiate the two, special names that will show up in a debugger like Visual Studio have been given to these two threads.  The OS controlled application main thread will have the name "**OS Main Thread**" and Unity's thread will have the name "**Unity Main Thread**".





