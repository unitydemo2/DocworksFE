PS Vita Profiling
===

## Unity Profiler
There are two ways to connect the Unity profiler to your running game.

The unity editor can attach automatically to your PSVita when doing a Build and Run.

1. In Build Settings set your Build Type to PC Hosted.
1. Tick the Development Build button.
1. Tick the Autoconnect Profiler button.
1. Click Build and Run to run your game on the device. The Unity profiler will automatically open and connect when the game starts.
1. Use the profiler as usual.

You can manually attach the Unity profiler to a running development build version of your game.

1. Run your development build on the device.
1. Open the Profiler window Windows-&gt;Profiler.
1. Select PSVIta Player (IP) as the active profiler.
1. Use the Profiler as usual.

See the standard Unity Profiler documentation form more information.

## Problems Connecting?

If you are having problems connecting the profiler to your device it's worth checking the following points:

1. Make sure the host pc and the devkit are on the same subnet (wifi)
1. Make sure multicast packets are allowed between wifi peers (no wifi peer isolation enabled)
1. In the devkit TTY locate the output regarding player connection for possibly helpful information
1. Verify IP address/port can be reached from hostpc (e.g. telnet &lt;ip&gt; &lt;port&gt;)
