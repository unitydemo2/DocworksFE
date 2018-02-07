#Upgrading Packages

Unity __Standard Assets__, __Asset Store__ downloads and assets in __Custom Packages__
 are all imported into projects via __packages__. 
See [Asset Packages](AssetPackages) for details, including how to import and export packages, as well as export updated packages.


Often __packages__ are updated by their makers; adding new files, removing files, or changing existing files. 
If you have already installed a __package__, you may want to upgrade your version to match a newer version.

When you import a __package__, 
Unity checks whether this is a newer version of an existing __package__, containing newer asset files (a re-install / upgrade) or a completely new package.
If Unity detects the __package__ is an upgrade, 
it gives you a  __Re-install__ option along with checkbox options of which asset files you want to re-install. 
These are detailed below in ***Re-install Situations***.

---------

###**Warning: Re-installing deletes files!**

When using the "re-install" option, Unity will delete all existing files associated with the package.

The way Unity determines which files will be deleted is by looking at the folders used for assets contained in the new package.

**Any existing folders in your project which match folders in the new package will have their contents deleted. There are possible undesired consequences to this if you use this option without carefully looking at what will be deleted.**

- If your package has an asset in a folder called "MyPackage", eg. `/Assets/MyPackage/Foo.fbx`, **all** assets in the *MyPackage* folder will be deleted and replaced with just the files from the new package.


- If you have added your own new files to an existing package folder, Unity will not differentiate between the genuine "old" package files, and files you may have subsequently added yourself. They will all be deleted.



- If the package you are re-installing contains assets in a folder shared by multiple packages, such as assets in `StreamingAssets/` or `Resources/`, Unity will not differentiate between the genuine "old" package files and files from other packages which put stuff in this same folder. They will be deleted.

- As a logical conclusion to these rules, if the package you are re-installing has assets in the root `Assets/` folder, and you have the "re-install" option enabled, **all** the assets in your project will be deleted and replaced with the package contents. You probably don't want this, and should disable the "re-install" option to avoid this outcome.


Use this option carefully!

------


When using the re-install option you should note that:

* The __Re-install__ checkbox is pre-selected.  

* Files to re-install are  pre-selected. 

If you leave the selections as they are, and click on __Import__, Unity deletes the existing, pre-selected files and installs new ones. 

This functionality ensures projects importing updated packages, particularly those from the __Asset Store__ and __Standard Assets__ which can be regularly updated, don't keep unused files in your project, such as duplicate files or 
old files that have been removed from the package.
However, it also means that it is easy to accidentally delete assets that you want to keep. 

If you are not sure about which asset files you want to re-install, you are strongly advised to back up any asset files away from the project's __Asset__ folder, 
via your computer's Finder (Mac) or File Finder (Windows) before re-installing/upgrading packages.

![Import Package dialog's Re-install Package option](../uploads/Main/UpgradePackagesCheckboxChecked5.png)

**Moving an Asset File or Package Folder**

If you move an element of a __package__ (that is the __package__ folder itself or a package's asset file) around inside the  package's parent folder, 
Unity can locate the moved element and offer re-install options. 
However, any elements of a __package__ which you move outside the asset package's parent folder, 
Unity no longer recognises as part of a __package__ and assumes a new install.

##Import and Re-install/Upgrade Options

Below are some example situations.

### Initial Import
For a brand new __package__, never imported before, in the __Import Package__ dialog box:

* All folders are expanded and checked by default.

* Each asset (including folders) is marked as NEW.

* There is no __Re-install__ option.
  
![All new asset files](../uploads/Main/UpgradePackagesNewPackageDialog.png)

### Changed Asset File Update

If a file has changed in the __package__, Unity displays the CHANGED icon against it.
For example:

*MyExamplePackage1* has an update to its asset *ExampleAssetA*. 
All the other assets are exactly the same as in the previous version of *MyExamplePackage1*; there is no change to their files.

In the __Import Package__ dialog box:

ExampleAssetA is marked as CHANGED. 
![CHANGED icon ](../uploads/Main/UpgradingPackagesChangedAsset.png)


* There is a __Re-install__ option. This is selected by default.


**[1]** With the __Re-install__ option **selected** (default):

* You can choose the unchanged asset files to update. (Selected to re-install is the default.)

* You can choose the updated asset file to re-install. (Selected to re-install is the default.)

![Re-install Package selected](../uploads/Main/UpgradePackagesCheckboxChecked5.png)

**[2]** With the __Re-install__ option **UNselected**:

* You cannot choose the unchanged asset files to re-install. They are greyed out.

* You can choose or unselect the updated asset file to re-install. (Selected to re-install is the default.)

![Re-install Package UNselected](../uploads/Main/ReinstallImportPackageCheckBoxUNchecked.png)

###New Asset File Update
If a file is new in the package, Unity displays the NEW icon against it.
For example:

MyExamplePackage1 has a new asset file; ExampleAssetB.
All the other assets are exactly the same as in the previous version of MyExamplePackage1; there is no change to their files.

In the __Import Package__ dialog box:

ExampleAssetB is marked as NEW. 
![NEW icon](../uploads/Main/UpgradePackagesNewAsset.png)

* There is a __Re-install__ option. This is selected by default. 
If you leave the __Re-install__ option selected, you have the option to re-install unchanged files, 
as described in ***Changed Asset File Update***, above.

* The new file's install is unaffected by the __Re-install__ option.


### Deleted Asset File Update
If a file has been deleted in the package, Unity displays the DELETED icon against it.
For example:

MyExamplePackage1 has been updated; ExampleAssetA has been removed.
All the other assets are exactly the same as in the previous version of MyExamplePackage1; there is no change to their files.

In the __Import Package__ dialog box:

ExampleAssetA is marked as DELETED.
![ ](../uploads/Main/UpgradePackagesDeletedAsset.png)

* There is a __Re-install__ option. This is selected by default. If you leave the __Re-install__ option selected, you have the choice to re-install unchanged files, 
as described in ***Changed Asset File Update***, above.

* Options:


    [A] To delete ExampleAssetA in your project, leave the __Re-install__ option selected.

    [B] To keep ExampleAssetA in your project, DE-select the  __Re-install__ option.


## Replacement Files & Packages

###Files

Each __package__ folder, sub-folder, and asset file in a __package__ has a unique identifier (a GUID). 
If a package's maker deletes an asset file in a version of their __package__, then, in a later version, 
replaces it with a file of the same name but uses an entirely new file as the replacement, the new file has a different GUID to the original.
In this case, Unity detects that the there is different file with a name conflict and displays a warning.  Here is an example:

ExampleAssetD has been removed from the package and later replaced with a different file.

In the __Import Package__ dialog box:

ExampleAssetD is marked as CHANGED. 
![CHANGED icon](../uploads/Main/UpgradePackagesChangedAsset.png)

ExampleAssetD is also marked with a WARNING. 
![WARNING icon](../uploads/Main/UpgradePackagesWarningAsset.png)

This warning is important: the replacement file may break links between the package and your project.


###Packages

Each __package__ folder, sub-folder, and asset file in a package has a unique identifier (a GUID). 
If you install a different __package__ with the same name as an existing one, the new __package__
 folder has a different GUID to the original.
In this case, Unity detects that the there is different __package__ with a name conflict and displays a warning. 
Unity assumes that the contents of the new package is replacing the existing __package__ and handles it as a re-install. Here is an example:

ExamplePackage1 is a new import; is a completely different package to ExamplePackage1 already installed. 
It has files; NewFile1, NewFile2. The existing ExamplePackage1 had two existing files; ExistingFile1, ExistingFile2.

In the __Import Package__ dialog box:

ExamplePackage1 folder is marked as CHANGED. ![ ](../uploads/Main/UpgradePackagesChangedAsset.png)

ExamplePackage1 folder is also marked with a WARNING. ![ ](../uploads/Main/UpgradePackagesWarningAsset.png)

NewFile1 and NewFile2 files are marked as NEW. ![ ](../uploads/Main/UpgradePackagesNewAsset.png)

ExistingFile1 and ExistingFile2 are marked as DELETED. ![ ](../uploads/Main/UpgradePackagesDeletedAsset.png)

**Note on the warning:** While, in this circumstance, the replacement folder may not break links in your project, take care to select the files you want for import and deletion.




<span class="meta-keywords">Search Words: Re-install Package, Re-install Standard Assets, Upgrade Standard Assets, Upgrade Package, Upgrading Standard Assets, Upgrading Package, Re-install Standard Assets, Re-install Package</span>
