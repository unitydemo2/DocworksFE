PSM Troubleshooting
====

This document describes troubles that frequently occur in development and how to handle them.

## The 0x808F1122 system error (-2138107614) occurs.

The following error may occur when creating a key or when deploying a Unity application to PS Vita.

````
"System error:(-2138107614),0x808F1122
HTTPS communication with the SCE server failed. Check whether the PC is correctly connected to the network. 
When executing with a company intranet environment, for example, please check that proxy server settings are correctly made."
````

When this error occurs, handle as follows.

**When a proxy server is not used**
* Select [Not use proxy server] from [Menu] - [File] - [Proxy Server Settings] of the Publishing Utility for Unity.

**When a proxy server is used**
* Select [Use proxy server] from [Menu] - [File] - [Proxy Server Settings] of the Publishing Utility for Unity and enter proxy server settings.

## Communication is not possible between the PC and PS Vita

When communication between the PC and PS Vita becomes impossible, check the following and handle as follows.

### Check Items

* The PC and PS Vita are correctly connected with the provided USB cable.
* PSM DevAssistant for Unity has been started in the PS Vita.
* The device driver of PS Vita is correctly installed on the PC.
* Note that the device driver can be confirmed with the following procedure.
    1. Open [Control Panel] - [Device Manager] .
    1. When PSM DevAssistant for Unity is not running, PlayStation&#174;Vita will be displayed in [Portable Devices] .
    1. When PSM DevAssistant for Unity is running, PSM USB Debug(COM1 - 256) will be displayed in [Ports (COM & LPT)] .

### Handling

* Terminate PSM DevAssistant on PS Vita.
* Terminate Unity Editor and Publishing Utility for Unity in the PC.
* Terminate PsmDeviceForUnity.exe in the PC.
    1. Press the Ctrl+Shift+Esc keys on the PC and open Windows Task Manager.
    1. Select the [Process] tab.
    1. Select PsmDeviceForUnity.exe in [Image Name] and execute [End Process] .

## Unity applications cannot be started on PS Vita

If Unity applications cannot be started on a PS Vita, check the following.

* The PS Vita can be connected to a Wi-Fi connection.

## A key mismatch error occurred

When a key mismatch error occurs, handle as follows.

1. Select [Menu] - [File] - [Build Settings] with the Unity Editor and open the [Build Settings] dialog.
1. Press the [Regenerate Keys] button and recreate the key.
1. Press the [Build] button or the [Build And Run] button and recreate the Unity app for PSM.

## MonoDevelop of Unity can no longer be started after installing the PSM SDK

When the PSM SDK is installed, there is a library problem where MonoDevelop for Unity can no longer be started.
In such cases, use the following countermeasure.

1. Open [Control Panel] - [Programs and Features] .
1. Select Gtk# for .Net 2.12.xx and uninstall it.

Note: In order to run PSM Studio in the PSM SDK, run gtk-sharp-2.12.xx.msi in C:/Program Files (x86)/SCE/PSM/software/ and re-install Gtk# for .Net 2.12.xx.

