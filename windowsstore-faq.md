FAQ
===================


###Unsupported classes and functions when using .NET Scripting Backend

* There are many classes and methods that are not supported in .NET for Windows Store Apps, see this link for supported classes: [http://msdn.microsoft.com/en-us/library/windows/apps/br230232.aspx](http://msdn.microsoft.com/en-us/library/windows/apps/br230232.aspx).

###How to create AppX package from Visual Studio ?

* After building the project from Unity Editor
* Open it with VS2012, VS2013 or VS2015
* In the solution explorer, right click on the project
* **Store** -&gt; **Create App Packages**
* Do you want to build packages to upload to the Windows Store? Choose No, then Next
* Pick appropriate platform, for ex., ARM Release
* Don't include public symbol files, this will make package smaller
* Create
* Locate folder which is named something like YourApp_1.0.0.0_ARM_Test, check that it has **Add-AppDevPackage.ps1** file
* Copy the folder contents to the target machine, then on the target machine right click on **Add-AppDevPackage.ps1** -&gt; **Run with PowerShell**
* Follow the steps, you might need an internet connection to install Developper License, this will require for you to have Microsoft account
* If everything is okay, your app should appear on the start menu

###How to install an appx file on your machine?

* Open **Windows PowerShell** from start menu, navigate to your appx file, execute **Add-AppxPackage &lt;yourappx&gt;.appx**, if the appx was signed, it will be installed on your machine. **Note:** if you're installing appx file again, you have to uninstall the previous one, simply right-click on the icon, and click Uninstall.

###I am getting an error "DEP0600: incorrect parameter" while deploying an application.

* Something is wrong with your certificate, try creating a new by clicking on **Package.appxmanifest** -&gt; **Packaging** -&gt; **Choose Certificate** -&gt; **Configure Certificate** -&gt; **Create Test Certificate**


###How to use Visual Studio's graphical debugger on ARM?

* Read this post [http://msdn.microsoft.com/en-us/library/hh780905(v=vs.110).aspx](http://msdn.microsoft.com/en-us/library/hh780905(v=vs.110).aspx) . You will need to create a WinRT component, and reference it from main module.

###If you have Windows N version (the one for Europe) and even the empty project doesn't run

* Install this (both x86 and x64):
    * If you have Windows 8.1 - [download link](https://www.microsoft.com/en-us/download/details.aspx?id=42503).
    * If you have Windows 10 - [download link](https://www.microsoft.com/en-us/download/details.aspx?id=48231).

###How to deploy a project on a tablet PC?

* Deployment on tablet PC is done via [Visual Studio Remote Debugger](http://msdn.microsoft.com/en-us/library/vstudio/bt727f1t.aspx)

###How do I choose which compiler to use for my C# scripts?

Under publishing settings on Windows Store player settings, there's a drop down menu called "Compilation overrides". There are 3 settings:

    1. None. All C# scripts will get compiled with Mono C# compiler;
    2. Use Net Core Partially. Scripts that are in folders “Assets/Plugins”, “Assets/Standard Assets” and “Assets/Pro Standard Assets” will get compiled with Mono C# compiler, while the rest will be compiled with Microsoft C# compiler;
    3. Use Net Core. All scripts will get compiled with Microsoft C# compiler.

Both compilers have their ups and downs. Compiling scripts with the Mono C# compiler will allow them to be referenced by JavaScript scripts, which, for example, is needed for Angry Bots (hence you have to set it to none). However, using the Microsoft C# compiler will allow you to use Microsoft specific APIs without the need for plugins - just wrap the code in #if NETFX_CORE/#endif, and it will compile and work just fine.

###Getting more information about Windows App Certification Kit (WACK) failure?

You can find a log in &lt;user&gt;\AppData\Local\Microsoft\AppCertKit which might contain additional information about the failure.

###Help! There's too many defines! Which are defined for which platform?

No worries. Here's all of them:

|:---|:---|
|__NETFX_CORE__|Defined on Windows Store 8.0, Windows Store 8.1, Windows Phone 8.1, Universal 8.1 and Universal 10 scripts that are compiled using Microsoft C# compiler.|
|__WINDOWS_UWP__|Defined on Universal Windows 10 scripts that are compiled using Microsoft C# compiler.|

See also [platform dependent compilation](PlatformDependentCompilation).

### Breakpoints in generated Assembly-CSharp-* projects aren't hit.

There could be couple of reasons:

* This may occur because of the JIT optimization on module load. In Visual Studio, go to __Tools__ > __Options__ > __Debugging__ > __General__ and uncheck __Suppress JIT optimization on module load__.
* Visual Studio doesn't consider Assembly-CSharp-* as your code. Go to __Tools__ > __Options__ > __Debugging__ > __General__ and uncheck __Enable Just My Code__. This tells Visual Studio that you want to debug the Assembly-CSharp-* projects.



