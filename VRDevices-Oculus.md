Oculus
======

<!-- https://trello.com/c/Qw7imxOL -->

##Getting started (Windows)

See the detailed documentation on the [Oculus Developer website](https://developer.oculus.com). In particular, follow the instructions for [using Unity with Oculus](https://developer3.oculus.com/documentation/game-engines/latest/concepts/book-unity/), and see the [recommended specs](https://developer.oculus.com/documentation/game-engines/latest/concepts/unity-req/) for Oculus development.

##Getting started (Gear VR)

You do not need to install anything extra on your machine to deploy to Gear VR. Follow the instructions at the [Samsung Developers' Website](https://resources.samsungdevelopers.com/Gear_VR_and_Gear_360).

Make sure that you can deploy a Unity app to your Galaxy Note 5, S6 Edge+, S6, or S6 Edge (see [Getting Started with Android Development](android-GettingStarted)):

1. Connect your Android device to your PC/Mac using a micro USB cable.
1. Create a new empty project (menu: __File &gt; New Project__).
1. Switch your build platform to Android (menu: File > Build Settings).
1. Open the Player Settings (menu: __Edit &gt; Project Settings &gt; Player__). Select Other Settings and check the Virtual Reality Supported checkbox.
1. Add Oculus to the Virtual Reality SDK’s list.
1. Create the folder ``Plugins/Android/assets`` under your project’s ``Assets`` folder (note: This folder name is case-sensitive).
1. Include an [Oculus signature file](https://developer.oculus.com/osig/) in your project in the ``Plugins/Android/assets`` folder.
1. Build and run. Insert the device into your headset and see the skybox with head tracking.

##Getting started (OpenVR)

Steam is required to run OpenVR applications, so install Steam and SteamVR. Once SteamVR is working properly with your headset, add OpenVR to the list of supported SDKs.  If you require additional functionality beyond Unity’s built-in support, see the [SteamVR asset store package](https://www.assetstore.unity3d.com/en/#!/content/32647).

##Inputs
See documentation on [Oculus Controllers](OculusControllers) for input control mapping. 




