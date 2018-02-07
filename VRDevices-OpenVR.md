# OpenVR

## Getting Started (OpenVR)
<!-- https://trello.com/c/Qw7imxOL -->

Steam is required to run OpenVR applications, so install Steam and SteamVR. Once SteamVR is working properly with your headset, add **OpenVR** to the list of supported SDKs (see below to learn how to do this). If you require additional functionality beyond Unity’s built-in support, see the [SteamVR asset store package](https://www.assetstore.unity3d.com/en/#!/content/32647).

##Supported Platforms
OpenVR is supported on the followng platforms:

* Windows
* macOS

###macOS Specific 

* Unity OpenVR on a macOS requires the Metal graphics and 64bit application target, OpenGL is not supported.

* OpenVR supports macOS 10.11.6 or later, but is optimized for macOS 10.13 High Sierra or later.

##Inputs
See documentation on [OpenVR Controllers](OpenVRControllers) for input control mapping. 

## Upgrading a project that contains the SteamVR Package

* Enable virtual reality support. Open the __Player Settings__ (menu: __Edit__ > __Project Settings__ > __Player__), select __Other Settings__ and check the __Virtual Reality Supported__ checkbox. 
* Use the __Virtual Reality SDK__ list displayed below the checkbox to add OpenVR.
* Enter Play Mode in the Editor to test the build.

---
* <span class="page-edit">2017-08-04  <!-- include IncludeTextAmendPageSomeEdit --></span>


* <span class="page-history">Supported platforms updated in [2017.2](https://docs.unity3d.com/2017.2/Documentation/Manual/30_search.html?q=newin20172) <span class="search-words">NewIn20172</span></span>


