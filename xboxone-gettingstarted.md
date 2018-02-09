Xbox One: Getting Started
=========================


To get started with Xbox One you first must be a registered, approved developer with Microsoft.  Next, start by setting up your development environment, covered in [Xbox One Setup](xboxone-setup).

Major Differences
-----------------

Xbox One, being a console has some unique differences than what is the norm for standalone and mobile platforms.  

Here is a general summary of some of the differences to be expected:

1. Ahead-Of-Time (AOT) compilation.
    * Scripts are AOT compiled and loaded in as normal Xbox One dynamic libraries. JITing is not supported.
    * Exotic class libraries (reflection, LINQ etc) not fully supported.
    * Read more details at [Xbox One: Ahead Of Time Compiler](xboxone-aot).
1. Fixed Resolution
    * Xbox One only supports 720P or 1080P.
1. No Fixed Function Shaders
    * Unity for Xbox One does not support Fixed Function shaders.
1. Native Plugins
    * The vast majority of Xbox One specific features are being developed as Native Plugins.  Documentation for Native Plugins is packaged with the Plugin Source.  You can download the Plugins [here](https://sites.google.com/a/unity3d.com/xbox-one-alpha/builds).

Process Lifetime Management
---------------------------

One of the first concepts you should become familiar with for Xbox One is the PLM.  The PLM is the system used to register for events such as your application being suspended, resumed or terminated.  You can read about the full details of PLM [here](xboxone-xboxoneplm).

Sandbox, TitleID and SCID
-------------------------

These three pieces of information are very important on Xbox One.  Since a great deal of information about a title is stored and dealt with in the cloud these values must be properly configured for things like Storage and Live Services to function properly.
You can read more infromation about all of these topics on [GDN](https://developer.xboxlive.com/en-US/Platform/Pages/home.aspx).

XDK
---

It is important that you use a version of the XDK that is supported by Unity.  You can find out more information about downloading and install XDKs on the [Setup](xboxone-setup) page.
