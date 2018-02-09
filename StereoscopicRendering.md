How to do Stereoscopic Rendering
================================

Stereoscopic rendering for DirectX11.1's stereoscopic 3d support.
----------------------------------------------------------------

The minimum requirements are:

* Windows 8.1.
* Unity Pro 4.5.
* Graphic card that supports Direct X 11.
* The graphics card driver needs to be set up with stereo support, and you need to use a dual DVI or DisplayPort cable, single DVI is not enough. 

The Stereoscopic checkbox in the Player Settings is strictly for DirectX11.1's stereoscopic 3d support. It doesn't currently use AMD's quad buffer extension. Make sure that [this sample](https://code.msdn.microsoft.com/windowsapps/Direct3D-111-Simple-Stereo-9b2b61aa) works on your machine. Stereo support works both in fullscreen and windowed mode.

When you launch the game, hold shift to bring up the resolution dialog. There will be a checkbox in the resolution dialog for Stereo3D if a capable display is detected. Regarding the API, there are a few options on Camera: stereoEnabled, stereoSeparation, stereoConvergence. Use these to tweak the effect. You will need only one camera in the scene, the rendering of the two eyes is handled by those parameters.

Note that this checkbox is not for Oculus (or other VR headsets to my knowledge) at this time.
     

1. Check your setup using [this sample](https://code.msdn.microsoft.com/windowsapps/Direct3D-111-Simple-Stereo-9b2b61aa).
2. Check the Stereoscopic Rendering and Use Direct3D 11 checkboxes in the Player Settings.
3. Publish it as 32-bit and 64-bit applications.
4. Try it with single camera and double cameras.
5. Hold Shift when launching the application to see Stereo 3D checkbox in the resolution dialog. The resolution dialog might be suppressed or always enabled depending on the project's player settings. 

Note: Currently, setting Unity to render in linear color space breaks stereoscopic rendering.  This appears to be a Direct3D limitation. It also appears that the ``camera.stereoconvergence`` param has no effect at all if you have some realtime shadows enabled (in forward rendering). In Deferred Lighting, you will get some shadows, but insconsistent between left & right eye.
 
 
Stereoscopic rendering for Oculus
---------------------------------
 
The Unity Free integration for Oculus is available from the [Oculus site](https://developer.oculus.com/downloads/). You can use Unity 4.6 upwards and the Oculus integration package to deploy all of your VR content to the Rift.

Getting started: import the Unity 4 Oculus integration package into Unity, then open up the demo scene and you're good to go.

The release supports Windows, Mac, Linux and Gear VR with full access to LibOVR through a pure C# wrapper.

Features include:

* High-quality in-editor VR previews
* Simple direct-to-Rift rendering
* Lens correction, TimeWarp, and dynamic prediction from LibOVR/VRLib
* Layered camera support for cockpits, UI, etc
* Cross-platform support for XInput controllers
* Consistent IPD and head model for comfort at all world scales
* Dynamic prediction with the DK2 Latency Tester
* Utilities for locomotion, Tracker access, and Rift status

See also the [Oculus Unity Integration Guide](http://static.oculus.com/sdk-downloads/documents/OculusUnityIntegrationGuide_0.4.3.pdf).

