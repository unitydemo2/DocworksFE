Profiling on the PSM
====

## Unity Profiler
There are two ways to connect the Unity profiler to your running game.

The Unity editor can attach automatically to your PSM when doing a Build &amp; Run.

1. Connect PSM to a Wi-Fi network.
1. Connect the PC running Unity Editor to the same Wi-Fi access point and make sure PSM and the PC are both in the same subnet.
1. In Build Settings set your Build Type to Dev Assistant
1. Tick the Development Build button
1. Tick the Autoconnect Profiler button
1. Click Build &amp; Run to run your game on the device. The Unity profiler will automatically open and connect when the game starts
1. Use the profiler as usual.

You can manually attach the Unity profiler to a running development build version of your game.

1. Connect PS Vita and PC to the same WiFi access point.
1. Start your development build on the device
1. Open the Profiler window Windows->Profiler.
1. Select PSM Player (IP) as the Active Profiler.
1. Use the profiler as usual.

More information about the Unity Profiler is available in the [Profiler documentation](Profiler).

##Problems Connecting?

If you are having problems connecting the profiler to your device it's worth checking the following points:

* Double-check that the host PC and PS Vita are on the same subnet (WiFi)
* Make sure multicast packets are allowed between WiFi peers (no wifi peer isolation enabled)
* If the PC is using a firewall, check that the port numbers 54998 to 55511 are released in [Send Rules].
* In the PSM console log locate the output regarding player connection for possibly helpful information
* Verify IP address/port can be reached from hostpc (e.g. telnet &lt;ip&gt; &lt;port&gt;)
* You can also use IP address and connect directly to the player using the Unity profiler (by selecting &lt;Enter IP&gt; in the Active Profiler list).

