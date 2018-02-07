#Cache Server

Unity has a completely automatic Asset pipeline. Whenever a source Asset like a .psd or an .fbx file is modified, Unity detects the change and automatically re-imports it. The imported data from the file is subsequently stored by Unity in an internal format.

This arrangement is designed to make the workflow as efficient and flexible as possible for an individual user. However, when working in a team, you may find that other users might keep making changes to Assets, all of which must be imported. Furthermore, Assets must be reimported when you switch between desktop and mobile build target platforms. The switch can therefore take a long time for large projects.

Caching the imported Assets data on the __Cache Server__ drastically reduces the time it takes to import Assets.

Each Asset import is cached based on: 

* The Asset file itself
* The import settings
* Asset importer version
* The current platform

If any of the above change, the Asset is re-imported. Otherwise, it is downloaded from the Cache Server.

When you enable the Cache Server (see _How to set up a Cache Server as a user_, below), you can even share Asset imports across multiple projects (that is, the work of importing is done on one computer and the results are shared with others).

Note that once the Cache Server is set up, this process is completely automatic, so there are no additional workflow requirements. It will simply reduce the time it takes to import projects without getting in your way.

##How to set up a Cache Server as a user

Setting up the Cache Server couldn't be easier. All you need to do is check Use Cache Server in the preferences and tell the local computer's __Unity Editor__ where the __Cache Server__ is. 

The Cache Server settings can be found in __Unity__ > __Preferences__ on Mac OS X or __Edit__ > __Preferences__ on Windows and Linux. 

![](../uploads/Main/CacheServerRemote.png)

To host the Cache Server on your local computer instead of a remote one, set __Cache Server Mode__ to  __Local__. 

![](../uploads/Main/CacheServerLocal.png)

This setting allows you to easily configure a Cache Server on your local machine. Due to hard drive size limitations, it is recommended you host the Cache Server on a separate computer. 


|**Property:** |**Function:** |
|:---|:---|
|__Cache Server Mode__|Select the Cache Server Mode you wish to use. This setting allows you to disable use of the Cache Server, specify a remote server, or set up a Cache Server on your local computer.|
|    _Disabled_ (default)| Do not use a Cache Server.|
|    _Remote_|Use a Cache Server hosted on a remote computer.|
|    _Local_|Use a local Cache Server on this computer.|
|__IP Address__ <br />(Remote only)| Specify the IP address of the remote machine hosting the Cache Server.|
|__Check Connection__ <br />(Remote only)| Use this button to attempt to connect to the remote Cache Server.|
|__Maximum Cache Size (GB)__ <br />(Local only)| Specify a maximum size in gigabytes for the Cache Server on this computer’s storage. The minimum size is 1GB. The maximum cache size is 200GB. The default is 10GB.|
|__Custom cache location__|Specify a location on disk to store the cache.|
|__Check Cache Size__<br/>(Local only)|Click this to find out how much storage the Local Cache Server is using. This operation can take some time to complete if you have a large project. The message “Cache size is unknown” is replaced with the cache size when it has finished running.|
|__Clean Cache__|Delete the contents of the cache.|

Unity displays the following warning if you have a Local Cache Server with a custom location, and that location becomes unavailable:

> _Local cache directory does not exist - please check that you can access the cache folder and are able to write to it_

##How to set up a __Cache Server__ as an administrator


Admins need to set up the __Cache Server__ computer that will host the cached Assets. 


You need to:

* Download the Cache Server. Go to the [Download Archive](https://unity3d.com/get-unity/download/archive) page. Locate the Unity version you use and click on the Downloads button for your target server’s operating system. Click the Cache Server link to start the download.
* Unzip the file, after which you should see something like this:

![](../uploads/Main/CacheServerZipCropped.png) 

* Depending on your operating system, run the appropriate command script.
* You will see a terminal window, indicating that the Cache Server is running in the background

![](../uploads/Main/CacheServerTerminal.png) 

The Cache Server needs to be on a reliable computer with very large storage (much larger than the size of the project itself, as there will be multiple versions of imported resources stored). If the hard disk becomes full the Cache Server could perform slowly.

##Installing the Cache Server as a service

The provided `.sh` and `.cmd` scripts must be set up as a service on the server.
The Cache Server can be safely killed and restarted at any time, since it uses atomic file operations.

##New and legacy Cache Servers

Two Cache Server processes are started by default. The legacy Cache Server works with versions of Unity prior to version 5.0. The new Cache Server works with versions of Unity from 5.0 and up. See Cache Server configuration, below for details on configuring, enabling, and disabling the two different Cache Servers.

##Cache Server configuration

If you simply start by executing the script, it launches the legacy Cache Server on port 8125 and the new Cache Server on port 8126. It also creates "cache" and "cache5.0" directories in the same directory as the script, and keep data in there. The cache directories are allowed to grow to up to 50 GB by default. You can configure the size and the location of the data using command line options, like this:

`./RunOSX.command --path ~/mycachePath --size 2000000000`

or 

`./RunOSX.command --path ~/mycachePath --port 8199 --nolegacy`

You can configure the Cache Server by using the following command line options:

* Use `--port` to specify the server port. This only applies to the new Cache Server. The default value is `8126`.
* Use `--path` to specify the path of the cache location. This only applies to the new Cache Server. The default value is `./cache5.0`.
* Use `--legacypath` to specify the path of the cache location. This only applies to the legacy Cache Server. The default value is `./cache`.
* Use `--size` to specify the maximum cache size in bytes for both Cache Servers. Files that have not been used recently are automatically discarded when the cache size is exceeded.
* Use `--nolegacy` to stop the legacy Cache Server starting. Otherwise, the legacy Cache Server is started on port `8125`.

##Requirements for the computer hosting the Cache Server

For best performance there must be enough RAM to hold an entire imported project folder. In addition, it is best to have a computer with a fast hard drive and fast Ethernet connection. The hard drive should also have sufficient free space. On the other hand, the Cache Server has very low CPU usage.

One of the main distinctions between the Cache Server and version control is that its cached data can always be rebuilt locally. It is simply a tool for improving performance. For this reason it doesn't make sense to use a Cache Server over the Internet. If you have a distributed team, you should place a separate Cache Server in each location.

The Cache Server runs optimally on a Linux or Mac OS X computer. The Windows file system is not particularly well-optimized for how the Cache Server stores data, and problems with file locking on Windows can cause issues that don't occur on Linux or Mac OS X.

##Cache Server FAQ

###Will the size of my Cache Server database grow indefinitely as more and more resources get imported and stored?
The Cache Server removes Assets that have not been used for a period of time automatically (of course if those Assets are needed again, they are re-created on next usage). 

###Does the Cache Server work only with the Asset server?

The Cache Server is designed to be transparent to source/version control systems, so you are not restricted to using Unity's Asset server.

###What changes cause the imported file to get regenerated?

When Unity is about to import an Asset, it generates an MD5 hash of all source data.

For a Texture, this consists of:

* The source Asset: "myTexture.psd" file
* The meta file: "myTexture.psd.meta" (Stores all importer settings)
* The internal version number of the Texture Importer
* A hash of version numbers of all [AssetPostprocessors](ScriptRef:AssetPostprocessor.html)

If that hash is different from what is stored on the Cache Server, the Asset is reimported. Otherwise the cached version is downloaded. The client Unity Editor only pulls Assets from the server as they are needed - Assets don't get pushed to each project as they change.

###How do I work with Asset dependencies?

The Cache Server does not handle dependencies. Unity's Asset pipeline does not deal with the concept of dependencies. It is built in such a way as to avoid dependencies between Assets. The [AssetPostprocessor](ScriptRef:AssetPostprocessor.html) class is a common technique used to customize the Asset importer to fit your needs. For example, you might want to add MeshColliders to some GameObjects in an .fbx file based on their name or tag.

It is also easy to use `AssetPostprocessor` to introduce dependencies. For example you might use data from a text file next to the Asset to add additional components to the imported GameObjects. This is not supported in the Cache Server. If you want to use the Cache Server, you have to remove dependency on other Assets in the project folder. Since the Cache Server doesn't know anything about the dependency in your postprocessor, it does not know that anything has changed, and thus uses an old cached version of the Asset.

In practice there are plenty of ways you can do Asset postprocessing to work well with the Cache Server. You can use:

* The Path of the imported Asset
* Any import settings of the Asset
* The source Asset itself, or any data generated from it passed to you in the Asset postprocessor.

###Are there any issues when working with Materials?
Modifying Materials that already exist might cause trouble. When using the Cache Server, Unity validates that the references to Materials are maintained, but because no postprocessing calls are invoked, the contents of the Material cannot be changed when a model is imported through the Cache Server. Because of this, you might get different results when importing with and without Cache Server. It is best never to modify Materials that already exist on disk.

###Are there any Asset types which are not cached by the server?

There are a few kinds of Asset data which the server doesn't cache. There isn't really anything to be gained by caching script files, so the server ignores them. Also, native files used by 3D modelling software (Maya, 3D Max, etc) are converted to FBX using the application itself. The Asset server does not cache the native file nor the intermediate FBX file generated in the import process. However, it is possible to benefit from the server, by exporting files as FBX from the modelling software and then adding those to the Unity project.
