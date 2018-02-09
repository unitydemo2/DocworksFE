Streaming Assets
================


Most assets in Unity are combined into the project when it is built. However, it is sometimes useful to place files into the normal filesystem on the target machine to make them accessible via a pathname. An example of this is the deployment of a movie file on iOS devices; the original movie file must be available from a location in the filesystem to be played by the `PlayMovie` function.

Any files placed in a folder called __StreamingAssets__ (case-sensitive) in a Unity project will be copied verbatim to a particular folder on the target machine. You can retrieve the folder using the [Application.streamingAssetsPath](ScriptRef:Application-streamingAssetsPath.html) property. It's always best to use `Application.streamingAssetsPath` to get the location of the __StreamingAssets__ folder, as it will always point to the correct location on the platform where the application is running.

The location of this folder varies per platform. Please note that these are case-sensitive:

* On a desktop computer (Mac OS or Windows) the location of the files can be obtained with the following code:


    	 path = Application.dataPath + "/StreamingAssets";

* On iOS, use:


    	 path = Application.dataPath + "/Raw";

* On Android, use:


    	 path = "jar:file://" + Application.dataPath + "!/assets/";


On Android, the files are contained within a compressed .jar file (which is essentially the same format as standard zip-compressed files). This means that if you do not use Unity's WWW class to retrieve the file, you need to use additional software to see inside the .jar archive and obtain the file.
    
**Note**: .dll files located in the __StreamingAssets__ folder don't participate in the compilation.

