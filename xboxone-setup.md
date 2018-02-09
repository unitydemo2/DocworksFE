Xbox One Setup
==============


To get started with Xbox One you first need to ensure you have the XDK and console properly setup.  The *XDK* is a software development kit and API that is installed on your PC.  The console gets flashed with what's called a *recovery*.  In addition to the *recovery*, there is a set of tools installed on the console called the *provision* which is dependent on the XDK you have installed on your PC. 

The best source of information for setting up your development environment can found on Microsoft's [GDN](https://developer.xboxlive.com/en-US/Platform/Pages/home.aspx) site.  A direct link to XDK and recovery downloads can be found on the [GDN Downloads page](https://developer.xboxlive.com/en-us/platform/development/downloads/Pages/home.aspx), which also has a link to Microsoft's *Getting Started guide*.

A summary of the steps to get a proper environment setup:
---------------------------------------------------------



1. Download and install the XDK supported by Unity.  The XDK supported by Unity can be found listed for each build on the [builds page](https://sites.google.com/a/unity3d.com/xbox-one-alpha/builds).
1. Setup the console and enable *Devkit Mode* in the *Devleoper Settings*. 
1. Identify the Tools IP addresses for the console.  These can be located on the Xbox One under Settings -&gt; Developer Settings -&gt; Tools IP.
1. Establish a connection between your PC and console.
	- Run the **Xbox One Manager** tool which was installed on your PC when you installed the XDK.
	- Click the *Add Console* button in the bottom left.
	- Enter the the Tools IP from step 3. 
	- Click *Add*.
1. You are now ready to deploy to the console from Unity.

Provisioning the Devkit
-----------------------

When you update the console with a new recovery, it also *provisions* it.  This installs development tools onto the console an OS that is used for your game when using push or pull deployment.  The *provision* is dependent on the XDK; different XDKs install different versions of the *provision* on the console. 

In order for Unity to work with the console, you must provision it using the XDK supported by Unity.  Unity has a prebuilt executable,  XboxOnePlayer.exe, that runs your game.  This executable is tied to the XDK, and using a *provision* from a different XDK can cause errors or crashes when running your game.

This isn't a problem for your game once it is released because your released version will be built as a package which has the important parts from the *provision* built into it.     


Supported XDK And Recovery Versions
-----------------------------------

The XboxOnePlayer.exe that runs your game is prebuilt with a specific version of the XDK.  The version is noted in the release notes and on Unity's Xbox One Google group's [build page](https://sites.google.com/a/unity3d.com/xbox-one-alpha/builds).

You must install the supported XDK on your PC and provision the console using that same XDK.  You can install a later recovery on your console, but only if you provision the devkit with the _xbprovision.exe_ from the earlier XDK, the one that Unity supports.

Updating to the latest recovery is always recommended.  XR testing always uses the latest available recovery.