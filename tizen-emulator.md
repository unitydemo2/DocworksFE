#Tizen Emulator

The Tizen SDK includes a virtual device Emulator. The Emulator provides the full stack of the Tizen platform, so that you can test Tizen applications before deploying them to the real target device. This is particularly useful if you don’t have a mobile device with which to port and test your game.

Learn more about the Tizen Emulator on the [Tizen Developer Emulator page](https://developer.tizen.org/development/tools/common-tools/emulator).

## Getting started

### Create an Emulator

1. Launch the Tizen Emulator Manager from your Tizen SDK installation. Click on __Create New Emulator__ and choose __mobile__.

	
    ![](../uploads/Main/TizenEmulator0.png)


2. Give your new Virtual Machine a name. Choose __mobile-2.4__ as the platform, and choose the size screen you would like emulated from the templates listed:

    ![](../uploads/Main/TizenEmulator1.png)

3. If you want to, you can also customize the Emulator’s properties. Note that on macOS in the __OpenGL ES Ver__ field, only the __v1.1 & v2.0__ option is supported.

    ![](../uploads/Main/TizenEmulator2.png)

### Start an Emulator

In the Emulator Manager, select the emulator that you wish to test on and press the __Start__ button. ![](../uploads/Main/TizenEmulator3.png)

![](../uploads/Main/TizenEmulator4.png)

### Assign a Tizen Deployment Target

To assign a Tizen Deployment Target, you must already have Tizen set as the target platform in Unity’s __Build Settings__. See [Setting up Unity to build to your Tizen device](tizen-setup) for more information. When Tizen is set up for your project, follow these steps:

1. In the Unity menu bar, go to __Edit__ > __Project Settings__ > __Player__. In the Player Settings in the Inspector window, expand the __Publishing Settings__ section. 

![](../uploads/Main/TizenEmulator5.png)

2. Click the __Discover__ button. In the window that appears, click the drop-down menu and select __Emulator__ to see a list of all available emulators.

![](../uploads/Main/TizenEmulator6.png)

3. Select an emulator shown in the window. You are now ready to deploy to the chosen Tizen Emulator. Note that the Emulator must be launched and started up to the home screen of the Virtual Machine before you may deploy to it. Deploying before the Emulator has finished starting up results in deployment errors.

## Differences between device and emulator

On macOS, the Emulator does not display some Scenes properly. The example below shows screenshots of the Unity demo game Angry Bots. In the following image, the top picture shows the Emulator, and the bottom is the same project on a Samsung Z3.

![](../uploads/Main/TizenEmulator7.png)

Other features such as webcam and gyro do not operate within the Emulator. 

