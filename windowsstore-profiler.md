Windows Store Apps: Profiler
=======================


You can connect Unity's profiler to running Windows Store Application. 
Perform the following steps:

* Go to **Player Settings** -> **Publishing Settings** -> **Capabilities**
* Enable Private Networks (Client & Server)
* Build Windows Store App Visual Studio solution from Unity.
* Build and run the application
* If you've checked **Autoconnect Profiler** checkbox, the profiler should connect automatically to Windows Store App, if not - you have to explicitly pick it in Unity (**Window** -&gt; **Profiler** -&gt; **Active Profiler**), for ex., MetroPlayerX86 (MyDevice)

**Note**: Profiler doesn't work on _Master_ configuration

**Note**: Due Windows Store Apps restrictions, you won't be able to connect the profiler if the application is running on the same machine. For ex., if you're running Unity editor and Windows Store App on the same PC, you won't able to connect. You have to run Unity editor on one machine, and Windows Store App on another machine.

**Note**: Also ensure that machine where Unity Editor is running and machine where Windows Store App is running - **are on the same subnet**.
