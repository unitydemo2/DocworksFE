#Getting started with PS4 development

## Developing for PS4

To develop for the PlayStation 4 (PS4), you must be a Registered PlayStation Developer and own the appropriate hardware. If you do not have a Unity license for PS4, contact your Sony Interactive Entertainment (SIE) account manager or producer via the scedev.net website. These licenses are provided to Registered PlayStation Developers completely free of charge.

All Unity-built PlayStation titles must have the Made with Unity logo on the start-up screen, landing page or main menu. Find the Made with Unity logo on the [Unity Brand Usage Guidelines](http://unity3d.com/public-relations/brand) page, along with simple guidelines and a design manual. Alternatively, you can use the built-in Made with Unity splash screen to meet this requirement.

## Requirements

Each build of Unity for PS4 has a set of minimum or recommended requirements specified in their release notes. There are three different version numbers you need to adhere to:

* The firmware PUP (PlayStation Update Package) on your hardware PS4 Development Kit ("devkit") or Test Kit (“testkit”).

* The PS4 Software Development Kit (SDK) version on your development machine.

* The version of SIE’s publishing tools.

PS4 Software Development Kits (SDKs) are only available for the 64-bit version of Windows, so you need to have a 64-bit version of the Unity Editor installed. There is no version of Unity for PS4 that uses either 32-bit or an alternative operating system (such as macOS or Linux).

## How Unity PS4 differs from desktop Unity

### Ahead-Of-Time (AOT) compilation

Scripts are AOT-compiled into a static library, which is subsequently linked with the Unity runtime to produce the player. Due to platform limitations, just-in-time (JIT) compilation is not supported. This means that you cannot use [C# ](https://msdn.microsoft.com/en-us/library/mt656691.aspx)[Reflection](https://msdn.microsoft.com/en-us/library/mt656691.aspx).

### Video formats

[Movie Textures](class-MovieTexture) are not available on PS4; instead, all video playback must use the functions contained within [UnityEngine.PS4.PS4VideoPlayer](ScriptRef:PS4.PS4VideoPlayer.html). An example of this is in the Editor after you have added the PS4 add-on installation, via __Assets__ > __Import Package__ > __PS4 Samples__ > __Video__. 
See PS4 DevNet’s [Video Data Encoding Tutorial](https://ps4.scedev.net/resources/documents/SDK/3.000/Video_Data_Encoding-Tutorial/0001.html) for more information on how to correctly encode your videos for playback on PS4.

### Shader semantics

If you have existing Unity projects that you wish to test on PS4, you need to apply a change to your Shaders. Without these changes, objects may be rendered in magenta, indicating a shader error.

The details of what to change are below. Note that any Shaders updated in this way continue to work on all platforms:

* v2f structures (output from vertex Shader used as input to fragment Shader) must be changed from `POSITION` to `SV_POSITION`. Note that a2v (application to vertex) structures should continue to use `POSITION`.

* Fragment Shader output that writes color must be changed from `COLOR` to `SV_Target`.

* Fragment Shader output that writes depth must be changed from `DEPTH` to `SV_Depth`.

* Do not use `sample` as a variable name in Shaders. This is a reserved word that causes Shaders to fail to compile if you use it incorrectly.

### Limited memory

The base console has a total of 8GB of unified memory. The Unity player and AOT-compiled script assemblies take away from the main memory. The PS4 system software also uses some of this memory, leaving you with approximately 4.5GB. 

Note that development consoles have 5.7GB of memory, so fitting in memory on a development console is no guarantee that your application works on a retail console.

PS4 Pro consoles have an additional 512MB, which is added to graphics memory (sometimes known as "the Garlic") when running in Pro mode.

## Access PS4’s unique functionality

Unity PS4 provides a number of new scripting APIs to access PSN services, input, native video support and much more. See the UnityEngine.PS4 section in the scripting API. For example, PS4 specific input is handled by the [PS4Input class](ScriptRef:PS4.PS4Input.html).

To access any PS4 SDK APIs that are not directly supported in the Unity API, write native C++ plug-in code and associated Unity script code to access the plug-in. For information on how to do this, see Unity’s [PS4 Samples](PS4Samples) of plug-ins covering the most commonly required areas.

## Useful links

* Getting Started Guide:
[https://ps4.scedev.net/docs/startup/1/](https://ps4.scedev.net/docs/startup/1/) 

* SDK Manager:
[https://ps4.scedev.net/docs/sdk_manager/1](https://ps4.scedev.net/docs/sdk_manager/1) 

* General Documentation:
%SCE_ROOT_DIR%\ORBIS\documentation\pdf\en 

* Publishing Documentation:
%SCE_ROOT_DIR%\ORBIS\Publishing\

* SCE Samples:
%SCE_ORBIS_SDK_DIR%\target\samples

