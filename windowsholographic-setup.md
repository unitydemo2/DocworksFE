#Set-up

##Project set-up

A Unity project for Microsoft Holographic platform isn't very different to a Unity project for other platforms, with a few notable exceptions:

* Ensure that the Camera you intend to track the HoloLens device's position is tagged as __Main Camera__ in the Inspector window. The default Camera in the Scene should already be tagged appropriately.  
* Set the __Main Camera__'s __Background__ property to __Solid Color__ rather than the defaulted __Skybox__. Set the background color to (0, 0, 0, 0).
* Use the __Fastest Quality Settings__ in __Edit__ > __Project Settings__ > __Quality__.  This maximizes performance and reduces power consumption. In particular, soft shadows and shadow cascades are too expensive to use on the HoloLens, and should be avoided.
* Enable the appropriate publishing flags based on which subsystems your application uses.

To learn more, see Microsoft's documentation on [Performance recommendations for Unity](https://dev.windows.com/en-us/holographic/Performance_recommendations_for_Unity).

##Publishing settings

The following capability flags are provided under __Player Settings__ > __Publishing Settings__. System features fail if you don't enable the appropriate capability flags. 

Not all of the publishing settings below are specific to Windows Holographic. For more information, see Unity's documentation on [WSA Player Settings](class-PlayerSettingsWSA).

| | |
|:---|:---|
|__PicturesLibrary__|Required for __PhotoCapture__ capture camera frame functionality.|
|__MusicLibrary__|Required for __VideoCapture__ audio recording functionality.|
|__VideosLibrary__|Required for __VideoCapture__ video recording functionality.|
|__WebCam__|Required for __PhotoCapture__ and __VideoCapture__.|
|__Microphone__|Required for voice recognition.|
|__SpatialPerception__|Required for Spatial Mapping.|


##Exporting a Visual Studio solution


Once you've built your project and are ready to test, export the project to a Visual Studio solution. To build for __Windows Holographic__, choose the following options under __File__ > __Build Setting__:

* __Platform: Windows Store__
* __SDK: Universal 10__
* __UWP Build Type: D3D or XAML__
* __Unity C# Projects__ (check this box)

Under __Player Settings__ > __Other Settings__:

* Enable __Virtual Reality Supported__.
* Click the __+__ button on the __Virtual Reality Devices__ list and select __Windows Holographic__.

Checking the __Unity C# Projects__ checkbox includes your scripting files in their own project in the generated solution. This allows you to conveniently edit and debug your scripts without needing to re-export from Unity. A re-export is only required if your project settings or content change. 

See Microsoft's documentation on [Exporting and building a Unity Visual Studio solution](https://dev.windows.com/en-us/holographic/Exporting_and_building_a_Unity_Visual_Studio_solution)  for more details.