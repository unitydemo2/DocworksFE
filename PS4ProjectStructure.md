#PS4 Project structure

## Mount points

### Writing access directories

Unlike PC or Standalone builds, the PlayStation 4 platform has restrictions on where you're allowed to write files to. Specifically, you do not have unrestricted access to the hard drive of the PS4; you only have access to write files to the mount points of [Application.persistentDataPath](ScriptRef:Application-persistentDataPath.html) (_download0_) and [Application.temporaryCachePath](ScriptRef:Application-temporaryCachePath.html) (_temp0_).

By default, there is no space in the mount point download0 available to an application; if you require this mount point, you need to reserve space. To do this, set the size of download0 via __Player Settings__ > __Publishing Settings__ > __Persistent Data Size__. Note that the size of download0 is limited to a maximum of 1024MB of data. If you plan to include over 1024MB of additional data, then you need to discuss this with Sony Interactive Entertainment (SIE, sometimes known as SCE), either via [Private Support](https://ps4.scedev.net/support/newissue) or through the [Accounts and Content Delivery forum](https://ps4.scedev.net/forums/forum/24/).

During development, when running a PC-hosted build, you can also write files to the _app0_ mount point via [Application.dataPath](ScriptRef:Application-dataPath.html) (_app0/Media_).

### Streaming Assets

[Application.streamingAssetsPath](ScriptRef:Application-streamingAssetsPath.html) is packaged to _app0/Media/StreamingAssets_. Use this for Assets that Unity should not process, like videos, AssetBundles and custom Assets.

### Plugins

Assets which you select for the PS4 platform in the [Plugin Inspector](PluginInspector) and have the file extensions **.sprx**, **.prx**, **\_suprx** or **\_stub.a** are packaged to _Media/Plugins/*_.

For more information on PS4 mount points, see the SDK documentation on [Application Requirements (File Organization)](https://ps4.scedev.net/resources/documents/SDK/latest/Application_Requirements_File_Organization/0001.html).

## The Resources folder

The _Resources_ folder allows you to refer to Assets by their file path, rather than custom references. 

Note that the entire _Resources_ folder is always included for your build and packaged into a single file, regardless of what’s actually used. On PlayStation 4, this can have two important side effects that you should be aware of early in development so that you can plan around them:

* If the files in your _Resources_ folder add up to a significant size, then the generated _resources.asset_ file is equally large. This is loaded during the transition into the first Scene in the project, so your game might spend a long time loading at the start. This first load is not performed asynchronously, so your game can’t enter a loading screen or show any animating or moving features as it loads. This can cause compliance issues with SIE’s Technical Requirements Checklist (TRC). See Sony’s [documented example of a TRC failure](https://ps4.scedev.net/resources/documents/TRC/1.5/TRC/R4018.html) to learn more.

* This _resources.asset_ file is always one single file, and if you ever release a patch for your game, the size of this patch will always contain the entire file. This means that even if you make a single, minor change, your patch file could be many hundreds of megabytes in size, because all of your Assets are in this single location.

For more information on how to manage this, please see Unity’s [Best practice guide to the Resources folder](https://unity3d.com/learn/tutorials/topics/best-practices/resources-folder).

