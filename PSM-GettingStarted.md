Getting started with Unity for PSM
===

This document explains the procedure for setting up the host PC.

## Installing Software

Install the following software in the development PC.

* Unity Editor, with "Unity for PSM" support
* PSM Tool Set for Unity

## Proxy Server Settings

When the development PC uses a proxy server with a company intranet environment, etc. to connect to a network, make settings as follows.

1. Install PSM Tool Set for Unity in the PC in advance.
1. Open Publishing Utility for Unity using the shortcut on the desktop.

    ![Figure 1.  Publishing Utility for Unity](../uploads/Main/PublishingUtilityforUnity.png) 

1.  Select [Menu] - [File] - [Proxy Server Settings] in Publishing Utility for Unity. A dialog will be displayed - make settings according to your environment.

    ![Figure 2.  Proxy server settings](../uploads/Main/ProxyServerSettings.png) 

## Create the Publisher Key

### About Publisher Key
A Publisher Key is a key that is allocated to a person with a Publisher License. The keys required for running apps will be generated based on this Publisher Key.

### Create the Publisher Key as follows.
1. Open Publishing Utility for Unity using the shortcut on the desktop, then select the [Key Management] panel.

    ![Figure 3.  Key Management panel](../uploads/Main/KeyManagementPanel.png) 

1. If a Publisher Key has not been registered, generate a Publisher Key with the [Generate Publisher Key] button or import a Publisher Key with the [Import Publisher Key] button.\\
Note: Publisher Keys are shared with the PSM SDK. Remember this if the Publisher Key is changed.

    ![Figure 4.  [Generate Publisher Key] button and [Import Publisher Key] butto](../uploads/Main/KeyManagementPanel_PubKey.png) 

1. When a Publisher Key has been generated or imported, information will be displayed for [Key Name] and [Date of Creation].

### Supplementary Notes on the Publisher Key

* The creation of the Publisher Key is only required once. The Publisher Key can be continually used even when the Unity Editor and PSM Tool Set are updated.
* A Publisher Key will be registered on SCE servers when created.
* Only the most recently created Publisher Key will be valid for a single SEN account. If developing with a team, note this when overwriting a Publisher Key. 

