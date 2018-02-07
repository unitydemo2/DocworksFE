Using External Version Control Systems with Unity
=================================================


Unity offers an [Asset Server](AssetServer) add-on product for easy integrated versioning of your projects and you can also use **Perforce** and **PlasticSCM** as external tools (see [Version Control Integration](Versioncontrolintegration) for further details). If you for some reason are not able use these systems, it is possible to store your project in any other version control system, such as Subversion or Bazaar. This requires some initial manual setup of your project. 

Before checking your project in, you have to tell Unity to modify the project structure slightly to make it compatible with storing assets in an external version control system. This is done by selecting __Edit-&gt;Project Settings-&gt;Editor__ in the application menu and enabling External Version Control support by selecting __Visible Meta Files__ in the dropdown for Version Control. This will show a text file for every asset in the `Assets` directory containing the necessary bookkeeping information required by Unity. The files will have a `.meta` file extension with the first part being the full file name of the asset it is associated with. Moving and renaming assets within Unity should also update the relevant `.meta` files. However, if you move or rename assets from an external tool, make sure to syncronize the relevant `.meta` files as well. 

When checking the project into a version control system, you should add the `Assets`, `UnityPackageManager` and the `ProjectSettings` directories to the system. The `Library` directory should be completely ignored - when using .meta files, it's only a local cache of imported assets.

When creating new assets, make sure both the asset itself and the associated `.meta` file is added to version control.

Example: Creating a new project and importing it to a Subversion repository.
----------------------------------------------------------------------------


First, let's assume that we have a subversion repository at ```svn://my.svn.server.com/``` and want to create a project at ```svn://my.svn.server.com/MyUnityProject```.
Then follow these steps to create the initial import in the system:


1. Create a new project inside Unity and call it `InitialUnityProject`. You can add any initial assets here or add them later on.
1. Enable __Visible Meta files__ in __Edit-&gt;Project Settings-&gt;Editor__
1. Quit Unity (this ensures that all the files are saved).
1. Delete the `Library` directory inside your project directory.
1. Import the project directory into Subversion. If you are using the command line client, this is done like this from the directory where your initial project is located:
```svn import -m"Initial project import" InitialUnityProject svn://my.svn.server.com/MyUnityProject``` 
If successful, the project should now be imported into subversion and you can delete the `InitialUnityProject` directory if you wish.
1. Check out the project back from subversion
```svn co svn://my.svn.server.com/MyUnityProject``` and check that the `Assets`, `UnityPackageManager` and `ProjectSettings` directory are versioned.
1. Open the checked out project with Unity by launching it while holding down the __Option__ or the left __Alt__ key. Opening the project will recreate the `Library` directory in step 4 above.
1. **Optional:** Set up an ignore filter for the unversioned `Library` directory:
```svn propedit svn:ignore MyUnityProject/``` 
Subversion will open a text editor. Add the Library directory.
1. Finally, commit the changes. The project should now be set up and ready:
```svn ci -m"Finishing project import" MyUnityProject```
