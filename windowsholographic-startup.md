#Running your first application

##Build your Project in Unity

1. Configure your content. Create your Unity Project as normal.
2. Configure __File__ > __Build Settings__ for HoloLens. See [Set-up](windowsholographic-setup) for details of these settings.
3. __Build your project in Unity.__ A successful build generates a Visual Studio solution containing your project and everything required to build and run on the device. An operating system window with the path to the solution should open automatically.

##Run from Visual Studio

1. Open the solution generated in step 3, above.
2. Specify device details. Choose __Release__, __x86__, and __Remote Machine__. Enter the IP of the device to run on, select __Universal (Unencrypted Protocol)__ for __Authentication Mode__.
3. Build the solution in Visual Studio. If there are no errors and the destination device is unpaired, the build continues until it displays a dialog window. The dialog window for a pairing number.
4. Pair with your HoloLens device:
    * On the device, choose __Settings__ > __Update (Device update, reset, developer)__ > __For Developers__ > __Pair__ which opens a dialog window containing a number. 
    * Enter this number into the Visual Studio dialog window.
    * The window with the pairing number on the device should present a __Done__ button when the device is paired.  Use a zooming Tap gesture on this button to continue: press thumb and forefinger together with a closed hand and then extend thumb and forefinger.
5. Deploy continues. Your application should now run.

**NOTE:** You should only need to pair once per machine, per device.