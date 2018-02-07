Windows 8.1 Universal Applications
==============================

|**WARNING: LEGACY DOCUMENTATION** |
|:---|
|Note that that from Unity 2017.1 this documentation is out-dated. 2017-06-30|

Windows 8.1 Universal Applications is a way to target both Windows Store and Windows Phone target with a - single Visual Studio project that works on both Windows 8.1 and Windows Phone 8.1: desktops, laptops, tablets and phones. It is a direct result of platform convergence movement.

You can read more about Windows 8.1 Universal Applications here: [http://dev.windows.com/en-us/develop/Building-universal-Windows-apps](http://dev.windows.com/en-us/develop/Building-universal-Windows-apps)

Unity exposes a way to build Universal Windows Store/Phone 8.1 applications, through selecting "Universal 8.1" SDK in build window. Upon building such a project, Unity creates a Universal Visual Studio project, which then can be built to both Windows and Windows Phone devices.

How does it work?
-----------------

Windows Phone 8.1 and Windows 8.1 are still not binary compatible - you cannot run a single DLL on both platforms unless it is a portable class library, which would mean you would not be able to access platform specific APIs on them (like SMS API on the Windows Phone and mouse API on Windows). Therefore, we compile two versions of assemblies.

There are two main differences between assemblies compiled for the phone and the store: preprocessor directives and target SDK. Windows gets to target Windows .NET Core, while the Phone targets Phone .NET Core. They're almost identical, although there are some very minor differences.

Universal Project folder structure looks like this:

    UniversalApp1 - (solution directory)
        UniversalApp1.Windows - (here goes windows specific files, all Windows DLLs)
            -
            -
            -
        UniversalApp1.WindowsPhone - (here goes windows phone specific files, all Windows Phone DLLs)
            -
            -
            -
        UniversalApp1.Shared - (here goes shared files)
            -
            -
            -

When you build a Universal Application, you will produce two binaries out of single project - one for Windows and one for Windows Phone. Neither AppX package has redundant files left from over the other platform - all thanks to the project structure.


<br/>
<br/>

----------
*  <span class="page-edit">2017-06-30  <!-- include IncludeTextAmendPageNoEdit --></span>