Universal Windows Platform: Profiler
=======================


You can connect Unity's profiler to running Universal Windows Application. 
Perform the following steps:

* Go to **Player Settings** -> **Publishing Settings** -> **Capabilities**
* Enable Private Networks (Client & Server)
* Build Universal Windows App Visual Studio solution from Unity.
* Build and run the application
* If you've checked **Autoconnect Profiler** checkbox, the profiler should connect automatically to Universal Windows App, if not - you have to explicitly pick it in Unity (**Window** -&gt; **Profiler** -&gt; **Active Profiler**), for ex., MetroPlayerX86 (MyDevice)

**Note**: Profiler doesn't work on _Master_ configuration

**Note**: Due Universal Windows Platform restrictions, you won't be able to connect the profiler if the application is running on the same machine. For ex., if you're running Unity editor and Universal Windows Platform on the same PC, you won't able to connect. You have to run Unity editor on one machine, and Universal Windows Platform on another machine. The only exception to this rule is "Autoconnect Profiler" build option, which makes the application connect to the editor instead.

**Note**: Also ensure that machine where Unity Editor is running and machine where Universal Windows App is running - **are on the same subnet**.

---
<span class="page-edit">• 2017-05-16  <!-- include IncludeTextAmendPageNoEdit --></span><br/>