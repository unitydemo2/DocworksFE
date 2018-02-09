About PsmDeviceForUnity.exe
===

This document explains the command line tool for interacting with the PSM DevAssistant for Unity, from the host PC.

## Overview

``PsmDeviceForUnity.exe`` is a command line tool installed with the PSM Tool Set for Unity.
It provides functionality to install / launch / uninstall applications in the DevAssistant, without using the Unity Editor.
Also, it enables the developer to inspect the console (TTY) output log from an application launched from the DevAssistant.

## The tool

``PsmDeviceForUnity.exe`` can normally be found under ``C:\Program Files\SCE\UnityForPSM``, or ``C:\Program Files (x86)\SCE\UnityForPSM``.
But a simpler way is to use the environment variable created when installing the PSM Tool Set for Unity - ``SCE_PSM_UNITY@``:

```
"%SCE_PSM_UNITY%\tools\PsmDevice\PsmDeviceForUnity.exe"
```

## Options

* Show connected devices
* Install application
* Launch application
* Uninstall application
* Reset DevAssistant
* Show Console Log

## Show connected devices

``PsmDeviceForUnity.exe -list_devices``

Display the list of the devices. First line shows number of the devices.
The first column shows the GUID which represent the device.
GUID .ex) ABCDEFGH-IJKL-MNOP-QRST-UVWXYZ012345

Example:

````
C:\>"&#37;SCE_PSM_UNITY&#37;\tools\PsmDevice\PsmDeviceForUnity.exe" -list_devices
1
aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee    Vita    on/off/drivererror     0????????????????
````

## Install application

``PsmDeviceForUnity.exe -install [GUID] [PackageFile] [ApplicationName]``

Install the package ( .psdp or .psmp ) to the target device ( GUID ).

Example:

````
C:\>"%SCE_PSM_UNITY%\tools\PsmDevice\PsmDeviceForUnity.exe" -install aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee application.psdp application_name
result[Install] = [0x00000000] OK
````

## Launch application

``PsmDeviceForUnity.exe -launch_unity [GUID] [ApplicationName]``

Launch specified application on the target device ( GUID ) .

Example:

````
C:\>"%SCE_PSM_UNITY%\tools\PsmDevice\PsmDeviceForUnity.exe" -launch_unity aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee application_name
result[LaunchUnity] = [0x00000000] OK
````

## Uninstall application

``PsmDeviceForUnity.exe -uninstall [GUID] [ApplicationName]``

Uninstall the application from the target device ( GUID ) .

Example:

````
C:\>"%SCE_PSM_UNITY%\tools\PsmDevice\PsmDeviceForUnity.exe" -uninstall aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee application_name
result[Uninstall] = [0x00000000] OK
````

## Reset DevAssistant

``PsmDeviceForUnity.exe -kill [GUID]``

Terminate the running application on the target device ( GUID ) .

Example:

````
C:\>"%SCE_PSM_UNITY%\tools\PsmDevice\PsmDeviceForUnity.exe" -kill aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee
result[Kill] = [0x00000000] OK
````

## Show Console Log

``PsmDeviceForUnity.exe -get_log [GUID]``

Display the console log output from the target device ( GUID ) .

Example:

````
C:\>"%SCE_PSM_UNITY%\tools\PsmDevice\PsmDeviceForUnity.exe" -get_log aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee
[2.800905] Initialize engine version: 4.3.4f1 (90588e819264)
[2.816761] CreateFromParsedShader : Default
[2.862128] CreateFromParsedShader : Sprites/Default
[2.984933] Begin MonoManager ReloadAssembly
[3.070849] Platform assembly: /UnityEngine.dll (this message is harmless)
[3.228958]
[3.270099] Non platform assembly: /Application/Data/Managed/Assembly-CSharp-firstpass.dll (this message is harmless)
[3.305092] Non platform assembly: /Application/Data/Managed/Assembly-CSharp.dll (this message is harmless)
[3.368999] Non platform assembly: /Application/Data/Managed/Assembly-UnityScript.dll (this message is harmless)
[3.541442] - Completed reload, in  0.556 seconds
[3.703088] CreateFromParsedShader : Hidden/Internal-GUITexture
[4.555144] CreateFromParsedShader : Hidden/Internal-Flare
[12.859599] CreateFromParsedShader : Hidden/Internal-GUITextureClip
[12.882330] 0: fps 0.12  ms/f 8301.66 [kernel avail main 124MB, cdram 0MB, phycont 26MB], [vram avail 86511KB / 106496KB], [monoMem peak 212KB, curr 212KB of 260KB]
````


