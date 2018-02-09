Creating and Running Unity for PSM Apps
===

## PS Vita Procedure

1. Connect the PSM to a PC using the USB cable included with the PSM.
1. Prepare the PSM for Internet connection.
1. Select the PSM DevAssistant for Unity icon in the PSM home screen to start DevAssistant.

  After DevAssistant starts, the following screen will be displayed.

  ![Figure 1.  PSM DevAssistant for Unity top menu](../uploads/Main/DevAssistantForUnity2.png) 

## Unity Editor Procedure

1. Start Unity Editor, open any Unity project with [Menu] - [File] - [Open Project...] , and select a scene.
1. Select [Menu] - [File] - [Build Settings] with the Unity Editor and open the [Build Settings] dialog.

    ![Figure 2.  Build Settings dialog](../uploads/Main/PSMBuildSettings.png) 

1. Select [PlayStation&#174;Mobile] in the [Platform] list, then press the [Switch Platform] button.
    * Press the [Add Current] button and add the scene to build.
    * Check the checkbox for the scene to build in the [Scenes In Build] list.

    ![Figure 3.  [Switch Platform] button, [Add Current] button, and [Scenes In Build] list](../uploads/Main/PSMBuildSettings2.png) 

1. Press the [Build And Run] button.

    When the button is pressed the folder where the psdp file is placed will open. Specify an arbitrary filename and save the file.
    * **psdp Files**
        * psdp files are package files for running in PS Vita and are Unity apps encrypted with a key.

    ![Figure 4.  [Build] and [Build And Run] buttons](../uploads/Main/PSMBuildSettings3.png) 

1. After pressing the Save button, the key generation, psdp file generation, and transfer/run in PS Vita procedure will be automatically performed.

    When the processing is successful, the Unity for PSM app will run in the PS Vita.

## Notes on updating the software

If any one of the following software is updated, regenerate the keys with the [Regenerate Keys] button in [Build Settings] .
If the keys are not regenerated, a key mismatch error will occur.

* Unity Editor
* PSM Tool Set for Unity
* PSM DevAssistant for Unity

