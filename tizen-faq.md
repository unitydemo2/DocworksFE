Tizen FAQ
================


Is the emulator supported?
---------------------------

No the Tizen emulator is not supported.


Obtaining Debug.Log output in realtime
-------------------------------------

Logs can be accessed in realtime while the game is running using the sdb tool.

````
./tizen-sdk/tools/sdb dlog Unity:*

````


What can I do to extend battery life?
-------------------------------------

If you are not using the Gyroscope, consider turning it off using:


````
Input.gyro.enabled = false;

````
in your game start-up code.

How can I manually deploy the TPK file to the device?
-----------------------------------------------------

The TPK file is the executable that the Unity build system creates for you. You can use Build and Run to build the TPK, transfer to the device, and then launch it for you. If you do not want to use Build and Run from the editor, you can use build to make the TPK only. To transfer the TPK to the device you can use a command line tool called `sdb`. This tool can be found in the `tools` folder in your Tizen SDK installation. Use a command line such as:


````
./tizen-sdk/tools/sdb install YourUnitySignedApp.tpk

````


How can I place my completed Unity project for sale on the Tizen Store?
----------------------------------------------------------------------------------

Full instructions can be found [here](http://www.tizenstore.com).
