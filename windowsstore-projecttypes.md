Windows Store Apps: Generated project with .NET scripting backend
=============================
Unity generates an XAML C# Visual Studio solution. With XAML C# solution generated you are able to use managed assemblies, such as UnityEngine.dll, Assembly-CSharp.dll, etc. with XAML code on top.

Unity will create files like resources, vcproj, xaml files. If you build a project on top of the same directory, these files will **not** be overwritten:

* Project files & solution files (.vcproj, .sln, etc.)
* Source files (App.xaml.cs, App.xaml.cpp)
* XAML files (App.xaml, MainPage.xaml, etc.)
* Image files (Assets\SmallTile.png, Assets\StoreLogo.png, etc.)
* Manifest file - Package.appxmanifest

It is safe for you to modify these files, and if you want to revert to previous state, just remove the file, and build your project on top of the folder.

**Note:** Unity doesn't modify solution and project files if they already exist on the disk. Visual Studio takes the whole Data folder, instead of individual files, so if new file is added to Data folder, it's automatically picked.

###Configurations

Generated Visual Studio projects have three configurations: **Debug**, **Release** and **Master**. **Debug** configuration has various safety checks and runs slower, **Release** configuration removes all those checks, but leaves profiler enabled. **Master** configuration should be used for final build that you submit to Store.

If you see **Development Build** text on the lower left corner, it means the game was not build for submission. This text will be shown, if you select **Development Build** when building form Unity, or if you've build **Debug** or **Release** configuration.

