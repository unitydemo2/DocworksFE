#Special folder names

You can usually choose any name you like for the folders you create to organise your Unity project. However, there are a number of folder names that Unity interprets as an instruction that the folder's contents should be treated in a special way. For example, you must place Editor scripts in a folder called __Editor__ for them to work correctly. 

This page contains the full list of special folder names used by Unity.


##Assets

The __Assets__ folder is the main folder that contains the Assets used by a Unity project. The contents of the Project window in the Editor correspond directly to the contents of the Assets folder. Most API functions assume that everything is located in the Assets folder, and so don't require it to be mentioned explicitly. However, some functions do need to have the Assets folder included as part of a pathname (for example, certain functions in the [AssetDatabase](ScriptRef:AssetDatabase.html) class).

##Editor

Scripts placed in a folder called __Editor__ are treated as Editor scripts rather than runtime scripts. These scripts add functionality to the Editor during development, and are not available in builds at runtime.

You can have multiple Editor folders placed anywhere inside the Assets folder. Place your Editor scripts inside an Editor folder or a subfolder within it.

The exact location of an Editor folder affects the time at which its scripts will be compiled relative to other scripts (see documentation on [Special Folders and Script Compilation Order](ScriptCompileOrderFolders) for a full description of this). Use the [EditorGUIUtility.Load](ScriptRef:EditorGUIUtility.Load.html) function in Editor scripts to load Assets from a Resources folder within an Editor folder. These Assets can only be loaded via Editor scripts, and are stripped from builds. 

**Note:** Unity does not allow components derived from MonoBehaviour to be assigned to GameObjects if the scripts are in the Editor folder.


##Editor Default Resources

Editor scripts can make use of Asset files loaded on-demand using the [EditorGUIUtility.Load](ScriptRef:EditorGUIUtility.Load.html) function. This function looks for the Asset files in a folder called __Editor Default Resources__.

You can only have one Editor Default Resources folder and it must be placed in the root of the Project; directly within the Assets folder. Place the needed Asset files in this Editor Default Resources folder or a subfolder within it. Always include the subfolder path in the path passed to the [EditorGUIUtility.Load](ScriptRef:EditorGUIUtility.Load.html) function if your Asset files are in subfolders.


##Gizmos

[Gizmos](ScriptRef:Gizmos.html) allow you to add graphics to the Scene View to help visualise design details that are otherwise invisible. The [Gizmos.DrawIcon](ScriptRef:Gizmos.DrawIcon.html) function places an icon in the Scene to act as a marker for a special object or position. You must place  the image file used to draw this icon in a folder called __Gizmos__ in order for it to be located by the DrawIcon function.

You can only have one Gizmos folder and it must be placed in the root of the Project; directly within the Assets folder. Place the needed Asset files in this Gizmos folder or a subfolder within it. Always include the subfolder path in the path passed to the [Gizmos.DrawIcon](ScriptRef:Gizmos.DrawIcon.html) function if your Asset files are in subfolders.


##Plug-ins

You can add [plug-ins](Plugins) to your Project to extend Unity's features. Plug-ins are native DLLs that are typically written in C/C++. They can access third-party code libraries, system calls and other Unity built-in functionality. Always place plug-ins in a folder called __Plugins__ for them to be detected by Unity.

You can only have one Plugins folder and it must be placed in the root of the Project; directly within the Assets folder.

See [Special folders and script compilation order](ScriptCompileOrderFolders) for more information on how this folder affects script compilation, and [Plugin Inspector](PluginInspector) for more information on managing plug-ins for different target platforms.


##Resources

You can load Assets on-demand from a script instead of creating instances of Assets in a Scene for use in gameplay. You do this by placing the Assets in a folder called __Resources__. Load these Assets by using the [Resources.Load](ScriptRef:Resources.Load.html) function.

You can have multiple Resources folders placed anywhere inside the Assets folder. Place the needed Asset files in a Resources folder or a subfolder within it. Always include the subfolder path in the path passed to the [Resources.Load](ScriptRef:Resources.Load.html) function if your Asset files are in subfolders. 

Note that if the Resources folder is an Editor subfolder, the Assets in it are loadable from Editor scripts but are stripped from builds.


##Standard Assets

When you import a Standard Asset package (menu: __Assets__ > __Import Package__) the Assets are placed in a folder called __Standard Assets__. As well as containing the Assets, these folders also have an effect on script compilation order; see the page on [Special Folders and Script Compilation Order](ScriptCompileOrderFolders) for further details.

You can only have one Standard Assets folder and it must be placed in the root of the Project; directly within the Assets folder. Place the needed Assets files in this Standard Assets folder or a subfolder within it.


##StreamingAssets

You may want the Asset to be available as a separate file in its original format although it is more common to directly incorporate Assets into a build. For example, you need to access a video file from the filesystem rather than use it as a MovieTexture to play that video on iOS. Place a file in a folder called __StreamingAssets__, so it is copied unchanged to the target machine, where it is then available from a specific folder. See the page about [Streaming Assets](StreamingAssets) for further details.

You can only have one StreamingAssets folder and it must be placed in the root of the Project; directly within the Assets folder.  Place the needed Assets files in this StreamingAssets folder or a subfolder within it. Always include the subfolder path in the path used to reference the streaming asset if your Asset files are in subfolders.


##Hidden Assets

During the import process, Unity completely ignores the following files and folders in the __Assets__ folder (or a sub-folder within it):

* Hidden folders.
* Files and folders which start with ‘**.**’.
* Files and folders which end with ‘**~**’.
* Files and folders named **cvs**.
* Files with the extension __.tmp__.

This is used to prevent importing special and temporary files created by the operating system or other applications.