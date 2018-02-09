PS4 Building and Running
=====

The following is a step by step guide to build and run a new project on the PS4.

## Before you start
* Make sure your copy of Windows is up to date, including Service Packs
* You must be a registered PS4 developer
* You should read [PS4 Getting Started](PS4GettingStarted) and [PS4 Setup](PS4Setup)

## Test a PC Standalone Build
To learn the basic steps necessary in creating a build we will first do a PC Standalone Build.

1. Create a new Unity project
1. Unity will create a new scene automatically
1. Save the new scene (File/Save Scene)
1. Open the Build Settings window (File/Build Settings)
1. Add your new scene to the 'Scenes to Build' pane either by clicking the 'Add Current' button or by dragging the scene from the Project View in to the 'Scenes to Build' window
1. Make sure 'PC, Mac & Linux Standalone' is selected in the Platform window
1. In the Target Platform option, select 'Windows'
1. Click the 'Build & Run' button
1. Choose a destination folder and give your game a filename. It is good practice to put your build in the project directory
1. The standalone executable should be created and executed. You will be prompted with a configuration dialog, click OK and the player will run.
1. Now you've gone through the basic build and run process you can now try a PS4 build



![](../uploads/Main/psvita_build_and_run_pc_standalone.jpg) 



## Build the PS4 Player
Continuing on from our previous exercise, Building and Running your new project on the PS4 is now very easy.

1. Firstly, ensure that your PS4 development kit is connected to your PC and powered on
1. Run Neighborhood for PlayStation(R)4 and ensure that the Connection Status is set to 'Connected' and that the device is currently the default device (displayed in bold)
1. In Unity, choose 'File/Build Settings...', then select 'PS4' in the Platform window and click the 'Switch Platform' button
1. Select PC Hosted as the 'Build Type'
1. Click on the 'Build & Run' button
1. Choose a destination folder (create a new folder). It is good practice to put your build in the project directory. If you are reusing the directory created in the last exercise you should delete the previously created .exe file. This is only required on this occasion because we've changed Platform
1. Unity should now build your project, automatically connect to your device and run the game


![](../uploads/Main/ps4_build_and_run.jpg) 

