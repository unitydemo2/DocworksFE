# Asset Packages

Unity __packages__ are a handy way of sharing and re-using Unity projects and collections of assets; 
Unity __Standard Assets__ and items on the Unity __Asset Store__ are supplied in packages, for example.  
__Packages__ are collections of files and data from Unity projects, or elements of projects, 
which are compressed and stored in one file, similar to Zip files. 
Like Zip files, a package maintains its original directory structure when it is unpacked, 
as well as meta-data about assets (such as import settings and links to other assets).

In Unity, the menu option __Export Package__ compresses and stores the collection, 
while __Import Package__ unpacks the collection into your currently open Unity project.

This page contains information on:

* Import Package:  - Standard Asset Packages  - Custom Packages
* Export Package
* Exporting Updated Packages


##Import Package
You can import __Standard Asset Packages__, which  are asset collections pre-made and supplied with Unity, 
and __Custom Packages__, which are made by people using Unity.


Choose __Assets > Import Package >__ to import both types of package.

![Fig 1: Asset>Import Package menu](../uploads/Main/ImportPackageMenu.png) 

###Standard Asset Packages
Unity __'Standard Assets'__ consist of several different packages: 
__2D, Cameras, Characters, CrossPlatformInput, Effects, Environment, ParticleSystems, Prototyping, Utility, Vehicles__.

To import a new __Standard Asset__ package:

1. Open the project you want to import assets into.

2. Choose __Assets > Import Package >__ plus the name of the package you want to import, 
and the __Import Unity Package__ dialog box displays, with all the items in the package pre-checked, 
ready to install. (See *Fig 2: New install Import Unity Package Dialog Box*.)

3. Select __Import__ and Unity puts the contents of the package into a __Standard Asset__ folder, 
which you can access from your __Project View__. 



![Fig 2: New install Import Unity Package dialog box](../uploads/Main/NewInstallImportPackageDialog.png) 


###Custom Packages
You can import custom packages which have been exported from your own projects or from projects made by other Unity users.

To import a new custom package:

1. Open the project you want to import assets into.

2. Choose __Assets > Import Package > Custom Package...__ to bring up up File Explorer (Windows) or Finder (Mac).

3. Select the package you want from Explorer or Finder, and the __Import Unity Package__ dialog box displays, 
with all the items in the package pre-checked, ready to install. (See *Fig 4: New install Import Unity Package dialog box*.)

4. Select __Import__ and Unity puts the contents of the package into the __Assets__ folder, 
which you can access from your __Project View__. 



![Fig 4: New install Import Unity Package dialog box](../uploads/Main/CustomPackageInstallDialog.png) 


##Export Package
Use __Export Package__ to create your own __Custom Package__.

1. Open the project you want to export assets from.
2. Choose __Assets > Export Package…__ from the menu to bring up the __Exporting Package__ dialog box.
(See *Fig 6: Exporting Package dialog box*.)
3. In the dialog box, select the assets you want to include in the package by clicking on the boxes so they are checked.
4. Leave the __include dependencies__ box checked to auto-select any assets used by the ones you have selected. 
5. Click on __Export__ to bring up File Explorer (Windows) or Finder (Mac) and choose where you want to store your package file. 
Name and save the package anywhere you like.

**HINT:** When exporting a package Unity can export all dependencies as well. 
So, for example, if you select a Scene and export a package with all dependencies, then all models, 
textures and other assets that appear in the scene will be exported as well. 
This can be a quick way of exporting a bunch of assets without manually locating them all.

![Fig 6: Exporting Package dialog box](../uploads/Main/ExportPackageDialog.png)

##Exporting Updated Packages
Sometimes you may want to change the contents of a package and create a newer, updated version of your asset package. 
To do this:

* Select the asset files you want in your package (select both the unchanged ones and the new ones).

* Export the files as described above in ***Export Package***, above. 

**NOTE:** You can re-name an updated package and Unity will recognise it as an update, so you can use incremental naming, for example: MyAssetPackageVer1, MyAssetPackageVer2.

**HINT:** It is not good practise to remove files from packages and then replace them with the same name:
Unity will recognise them as different and possibly conflicting files and so display a warning symbol when they are imported.
If you have removed a file and then decide to replace it, it is better to give it a different, but related name to the original.
