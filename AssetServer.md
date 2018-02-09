Asset Server (Team License)
=======================

Unity Asset Server Overview
---------------------------

Please be aware that the __Asset Server__ is now a legacy product. We recommend using __Plastic SCM__ or __Perforce__ for version control in your Unity project.

[PlasticSCM](plasticSCMIntegration)
[PerForce](perForceIntegration)

The __Unity Asset Server__ is an asset and version control system with a graphical user interface integrated into Unity. It is meant to be used by team members working together on a project on different computers either in-person or remotely. The Asset Server is highly optimized for handling large binary assets in order to cope with large multi gigabyte project folders. When uploading assets, __Import Settings__ and other meta data about each asset is uploaded to the asset server as well. Renaming and moving files is at the core of the system and well supported.

It is available only for Team License users. To purchase Team License (if you do not have it as part of Unity Pro) please visit the Unity store at [http://unity3d.com/store](http://unity3d.com/store)

Note that Asset Server is a legacy product and is no longer maintained.

New to Source Control?
----------------------


If you have never used Source Control before, it can be a little unfriendly to get started with any versioning system. Source Control works by storing an entire collection of all your assets - meshes, textures, materials, scripts, and everything else - in a database on some kind of server. That server might be your home computer, the same one that you use to run Unity. It might be a different computer in your local network. It might be a remote machine colocated in a different part of the world. It could even be a virtual machine. There are a lot of options, but the location of the server doesn't matter at all. The important thing is that you can access it somehow over your network, and that it stores your game data.

In a way, the Asset Server functions as a backup of your Project Folder. You do not directly manipulate the contents of the Asset Server while you are developing. You make changes to your Project locally, then when you are done, you __Commit Changes__ to the Project on the Server. This makes your local Project and the Asset Server Project identical.

Now, when your fellow developers make a change, the Asset Server is identical to their Project, but not yours. To synchronize your local Project, you request to __Update from Server__. Now, whatever changes your team members have made will be downloaded from the server to your local Project.

This is the basic workflow for using the Asset Server. In addition to this basic functionality, the Asset Server allows for rollback to previous versions of assets, detailed file comparison, merging two different scripts, resolving conflicts, and recovering deleted assets.

Setting up the Asset Server
---------------------------


The Asset Server requires a one time server setup and a client configuration for each user. You can read about how to do that in the [Asset Server Setup page](SettinguptheAssetServer).

The rest of this guide explains how to deploy, administrate, and regularly use the Asset Server.


##Daily use of the Asset Server



This section explains the common tasks, workflow and best practices for using the Asset Server on a day-to-day basis.


Getting Started
---------------


If you are joining a team that has a lot of work stored on the Asset Server already, this is the quickest way to get up and running correctly.


1. Create a new empty Project with no packages imported
1. Go to __Edit-&gt;Project Settings-&gt;Editor__ and select __Asset Server__ as the version control mode
1. From the menubar, select __Window-&gt;Version Control__
1. Click the __Connection__ button
1. Enter your user name and password (provided by your Asset Server administrator)
1. Click __Show Projects__ and select the desired project
1. Click __Connect__
1. Click the __Update__ tab
1. Click the __Update__ button
1. If a conflict occurs, discard all local versions
1. Wait for the update to complete
1. You are ready to go


Workflow Fundamentals
---------------------


When using the Asset Server with a multi-person team, it is generally good practice to Update all changed assets from the server when you begin working, and Commit your changes at the end of the day, or whenever you're done working. You should also commit changes when you have made significant progress on something, even if it is in the middle of the day. Committing your changes regularly and frequently is recommended.


Understanding the Server View
-----------------------------


The __Server View__ is your window into the Asset Server you're connected to. You can open the Server View by selecting __Window-&gt;Version Control__.


![The __Overview__ tab](../uploads/Main/AssetServer-ServerView.png) 


The Server View is broken into tabs: __Overview__ __Update__, and __Commit__. __Overview__ will show you any differences between your local project and the latest version on the server with options to quickly commit local changes or download the latest updates. __Update__ will show you the latest remote changes on the server and allow you to download them to your local project. __Commit__ allows you to create a __Changeset__ and commit it to the server for others to download.


###Connecting to the server

Before you can use the asset server, you must connect to it. To do this you click the __Connection__ button, which takes you to the connection screen:


![The Asset Server connection screen](../uploads/Main/AssetServer-Connection.png) 

Here you need to fill in:

1. Server address
1. Username
1. Password

By clicking __Show projects__ you can now see the available projects on the asset server, and choose which one to connect to by clicking __Connect__. Note that the username and password you use can be obtain from your system administrator. Your system administrator created accounts when they installed Asset Server.


###Updating from the Server

To download all updates from the server, select the __Update__ tab from the Overview tab and you will see a list of the latest committed Changesets. By selecting one of these you can see what was changed in the project as well as the provided commit message. Click __Update__ and you will begin downloading all Changeset updates.


![The __Update__ Tab](../uploads/Main/AssetServer-UpdateTab.png) 

###Committing Changes to the Server

When you have made a change to your local project and you want to store those changes on the server, you use the top __Commit__ tab.



![The __Commit__ tab](../uploads/Main/AssetServer-UploadAssets.png) 

Now you will be able to see all the local changes made to the project since your last update, and will be able to select which changes you wish to upload to the server. You can add changes to the changeset either by manually dragging them into the changeset field, or by using the buttons placed below the commit message field. Remember to type in a commit message which will help you when you compare versions or revert to an earlier version later on, both of which are discussed below. 


###Resolving conflicts

With multiple people working on the same collection of data, conflicts will inevitably arise. Remember, there is no need to panic! If a conflict exists, you will be presented with the __Conflict Resolution__ dialog when updating your project.


![The __Conflict Resolution__ screen](../uploads/Main/AssetServer-ResolveConflict.png) 

Here, you will be informed of each individual conflict, and be presented with different options to resolve each individual conflict. For any single conflict, you can select __Skip Asset__ (which will not download that asset from the server), __Discard My Changes__ (which will completely overwrite your local version of the asset) or __Ignore Server Changes__ (which will ignore the changes others made to the asset and after this update you will be able to commit your local changes over server ones) for each individual conflict. Additionally, you can select __Merge__ for text assets like scripts to merge the server version with the local version.

**Note:** If you choose to discard your changes, the asset will be updated to the latest version from the server (i.e., it will incorporate other users' changes that have been made while you were working). If you want to get the asset back as it was when you started working, you should revert to the specific version that you checked out. (See _Browsing revision history and reverting assets_ below.)

If you run into a conflict while you are committing your local changes, Unity will refuse to commit your changes and inform you that a conflict exists. To resolve the conflicts, select __Update__. Your local changes will not automatically be overwritten. At this point you will see the __Conflict Resolution__ dialog, and can follow the instructions in the above paragraph.


###Browsing revision history and reverting assets

The Asset Server retains all uploaded versions of an asset in its database, so you can revert your local version to an earlier version at any time. You can either select to restore the entire project or single files. To revert to an older version of an asset or a project, select the Overview tab then click __Show History__ listed under Asset Server Actions. You will now see a list of all commits and be able to select and restore any file or all project to an older version. 


![The __History__ dialog](../uploads/Main/AssetServer-RevertingAsset.png) 

Here, you can see the version number and added comments with each version of the asset or project. This is one reason why descriptive comments are helpful. Select any asset to see its history or __Entire Project__ for all changes made in project. Find revision you need. You can either select whole revision or particular asset in revision. Then click __Download Selected File__ to get your local asset replaced with a copy of the selected revision. __Revert All Project__ will revert entire project to selected revision.

Prior to reverting, if there are any differences between your local version and the selected server version, those changes will be lost when the local version is reverted.

If you only want to abandon the changes made to the local copy, you don't have to revert. You can discard those local modifications by selecting __Discard Changes__ in the main asset server window. This will immediately download the current version of the project from the server to your local Project.


###Comparing asset versions

If you're curious to see the differences between two particular versions you can explicitly compare them. To do this, open __History__ window, select revision and asset you want to compare and press __Compare to Local Version__. If you need to compare two different revisions of an asset - right click on it, in the context menu select __Compare to Another Revision__ then find revision you want to compare to and select it. 

_Note_: this feature requires that you have one of supported file diff/merge tools installed. Supported tools are:

* On Windows:
    * TortoiseMerge: part of [TortoiseSVN](http://tortoisesvn.net/) or a separate download from the [project site](http://sourceforge.net/project/showfiles.php?group_id=138498).
    * [WinMerge](http://winmerge.org/).
    * [SourceGear Diff/Merge](http://www.sourcegear.com/diffmerge/).
    * [Perforce Merge (p4merge)](http://www.perforce.com/perforce/products/merge.html): part of Perforce's visual client suite (P4V).
    * [TkDiff](http://sourceforge.net/projects/tkdiff/).
* On Mac OS X:
    * [SourceGear Diff/Merge](http://www.sourcegear.com/diffmerge/).
    * FileMerge: part of Apple's [XCode development tools](http://developer.apple.com).
    * [TkDiff](http://sourceforge.net/projects/tkdiff/).
    * [Perforce Merge (p4merge)](http://www.perforce.com/perforce/products/merge.html): part of Perforce's visual client suite (P4V).


###Recovering deleted assets

Deleting a local asset and committing the delete to the server will in fact not delete an asset permanently. Just as any previous version of an asset can be restored through __History__ window from the Overview tab.


![The __History__ dialog](../uploads/Main/AssetServer-RecoverDeleted.png) 

Expand __Deleted Assets__ item, find and select assets from the list and hit __Recover__, the selected assets will be downloaded and re-added to the local project. If the folder that the asset was located in before the deletion still exists, the asset will be restored to the original location, otherwise it will be added to the root of the Assets folder in the local project.


###Best Practices & Common Issues

This is a compilation of best practices and solutions to problems which will help you when using the Asset Server:


1. Backup, Backup, Backup
    * Maintain a backup of your database. It is very important to do this. In the unfortunate case that you have a hardware problem, a virus, a user error, etc you may loose all of your work. Therefore make sure you have a backup system in place. You can find lots of resources online for setting up backup systems.


1. Stop the server before shutting the machine down
    * This can prevent "fast shutdowns" from being generated in the PostgreSQL (Asset Server) log. If this occurs the Asset Server has to do a recovery due to an improper shut down. This can take a very long time if you have a large project with many commits.


1. Resetting you password from Console
    * You can reset your password directly from a shell, console or command line using the following command:
  

	 psql -U unitysrv -d template1 -c"alter role admin with password 'MYPASSWORD'" 


1. Can't connect to Asset Server
    * The password may have expired. Try resetting your password.
    * Also the username is case sensitive: "Admin" != "admin". Make sure you are using the correct case.
    * Make sure the server is actually running:
        * On OS X or Linux you can type on the terminal: ps -aux
        * On Windows you can use the Task Manager.
    * Verify that the Asset Server is not running on more than one computer in your Network. You could be connecting to the wrong one.


1. The Asset Server doesn't work in 64-bit Linux
    * The asset server can run OK on 64-bit Linux machines if you install 32-bit versions of the required packages. You can use "dpkg -i --force-architecture" to do this.


1. Use the Asset Server logs to get more information
    * Windows:
        * `ProgramFiles\Unity\AssetServer\log`
    * OS X:
        * `/Library/UnityAssetServer/log`


1. "The application failed to initialize properly (0xc0000135)" in Windows XP
    * In this case Service Pack 2 is required, and you should install .NET 2.0.


Asset Server training complete
------------------------------


You should now be equipped with the knowledge you need to start using the Asset Server effectively. Get to it, and don't forget the good workflow fundamentals. Commit changes often, and don't be afraid of losing anything.

