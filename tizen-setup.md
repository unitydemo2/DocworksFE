Setting up to build a Tizen device
=====================================================


To get your first project running on your Tizen device you will need to follow these steps.

1. Install the Tizen SDK.
    * Check the proper version of Tizen SDK depending on Samsung Z models from Samsung Developers site [developer.samsung.com](http://developer.samsung.com/samsung-z).
    * Download the Tizen SDK from the Tizen developer site [developer.tizen.org](http://developer.tizen.org/development/tizen-studio/download).
    * Instructions for installation are on [developer.tizen.org](http://developer.tizen.org/development/tizen-studio/download/installing-tizen-studio).

2. Download and Install the Tizen Certificate Extension SDK:
    * The Extension SDK is on the [Getting the Certificates](http://developer.samsung.com/z/develop/getting-certificates) section of the Samsung Developers site.
    * The installation instructions are on the [Install](http://developer.samsung.com/z/develop/getting-certificates/install) section of the Samsung Developers site.

3. Enable USB debugging on your device.
	1.  Start up your device.
	2.  Launch the Phone app from the home screen.
	
		![](../uploads/Main/tizenhomescreen.png)

	3.  Type *#84936# - The numbers 84936 spell out TIZEN.
	
		![](../uploads/Main/tizenkeypad.png) 

	4.  A menu displays. Tap the button on the right to enable __Developer Option__.
	
		![](../uploads/Main/tizendevoption.png) 
	5.  Press the __Home__ button to return to home screen.
	6.  Press and hold the __Home__ button to show recent apps.
	7.  Swipe across on the Settings app to close it.
	8.  Press the __Home__ button to return to the home screen.
	9.  Launch the Settings app.
	10.  Scroll to the bottom and select __Developer Options__.
	11.  Enable the __USB debugging__ option.
	
		![](../uploads/Main/tizenusbdebugging.png) 

4. Create a signing certificate.
    * Find directions for creating a signing certificate via the Tizen IDE. Open menu: __Help__ &gt; __Help Contents__ and click on the __Certificates__ topic in the navigation pane on the left side.
5. Set up the Tizen CLI environment.
    * Before you can deploy to a device, the Tizen Command Line Interface needs to know where the signing profiles configuration is located. You can run the following command in a terminal to set it up properly.
	
    Windows:

    ````
    C:\tizensdk-path\tools\ide\bin\tizen.bat cli-config "default.profiles.path=C:\workspace-path\.metadata\.plugins\org.tizen.common.sign\profiles.xml"
	````

    OS X:

    ````
    /tizensdk-path/tools/ide/bin/tizen.sh cli-config default.profiles.path=/path/to/workspace/.metadata/.plugins/org.tizen.common.sign/profiles.xml
	````
	
    In both cases you should replace `workspace-path` with the path to the Tizen IDE workspace that you created when you first launched the Tizen IDE and `tizensdk-path` with the full path to where your Tizen SDK is installed.
    

    **Note** 
    On Windows, you must run the command must from within the directory of a Tizen IDE project. Launch the Tizen IDE and create a Tizen Native Application project. 
    

    **Example**

    In the example below,  `TestApp` is your project.
	
    If your workspace is at `C:\workspace` and the Tizen SDK is installed at `C:\tizen-sdk`, then open a command prompt and then run the following commands:

    ````
    cd C:\workspace\TestApp
	
    C:\tizen-sdk\tools\ide\bin\tizen.bat cli-config "default.profiles.path=C:\workspace\.metadata\.plugins\org.tizen.common.sign\profiles.xml"
	````
	
6. Launching your game.
    1. In the Unity Editor, go to  __File__ &gt; __Build settings...__.
    2. Switch to the Tizen platform. 
    3. Ensure that __Development build__ is checked.  
    4. Next click on __Player Settings__. 
    5. Under __Publishing Setting__ enter the name of the signing profile that you created in the Tizen IDE. If you didn't give it a custom name or rename it in the IDE, then you should enter "default". 
    6. Click the __Build and Run__ button. 
Unity makes the game for you and deploys it to the device. The game then starts up on the device. 
