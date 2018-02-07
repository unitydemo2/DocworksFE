# PS4 profiling

This page provides information on how to connect your PS4 build to the Unity profiler, and other ways of profiling your build. See documentation on the [Unity Profiler](https://docs.unity3d.com/Manual/Profiler.html) for a comprehensive overview of the built-in profiler.

Connect your build to the Unity Profiler via the following steps:

1. Build and run a development build on the target machine (see documentation on [Building and running PS4 builds](PS4BuildingampRunning) to learn how to do this). Profiling can only be carried out on development builds; master builds cannot be profiled.

2. In the Unity Editor, navigate to __Windows__ > __Profiler__.

3. Open the __Active Profiler__ drop-down and select __PS4 Player__. Multiple listings of this appear if you have several devkits active on your network, so make sure you choose the IP address appropriate to your target.

The Profiler is now connected to the build, and you can begin profiling.

As an alternative to step 3, you can tick the __Autoconnect Profiler__ checkbox in __Build Settings__. This automatically connects the profiler as soon as the build is launched on the target machine.

## PlayStation 4 SDK tools

PlayStation 4 development gives you access to several high quality tools to allow you to profile your title during development. We highly recommend that you use these tools during PS4 development.

### Razor CPU

This tool allows you to perform captures of your build’s CPU activity, and then store and re-read that data. Because the information is not displayed in real-time during profiling, there is very little overhead in the captured data, resulting in a more accurate assessment of where CPU time is being spent. For more information, see documentation on [Profiling with Razor](PS4ProfilingWithRazor) and the [Razor CPU user's guide](https://ps4.scedev.net/resources/documents/SDK/latest/Razor_CPU-Users_Guide/__document_toc.html) ([https://ps4.scedev.net](https://ps4.scedev.net)).

### Razor GPU

This is a performance analysis and debugging tool that allows you to analyze GPU captures. For more information, see the [Razor GPU user's guide](https://ps4.scedev.net/resources/documents/SDK/latest/Razor_GPU-Users_Guide/__document_toc.html) ([https://ps4.scedev.net](https://ps4.scedev.net)).

### Memory Analyzer

The PlayStation 4 Memory Analyzer allows the tracking of allocations and de-allocations of memory to help in finding areas within your title where memory usage may be high, and also help find any potential memory leaks. For more information, see the [Memory Analyzer User's Guide](https://ps4.scedev.net/resources/documents/SDK/latest/Memory_Analyzer-Users_Guide/__document_toc.html) ([https://ps4.scedev.net](https://ps4.scedev.net)).

## Troubleshooting connection issues

If you are having problems connecting the Unity Profiler to your device, check that the network is set up as follows:

To get your build onto a PS4 devkit (and to see the console on the __Network Neighborhood__ for PlayStation 4), you need:

* An ethernet cable connected to the unlabeled (DEV) port on the back of your console. The IP address of this connection is displayed in the top-left corner of the system software’s home screen.

* A separate network connection with internet access, so that you can sign in to PSN to use the Profiler. This can be done either wirelessly or via the LAN port on the back of the console. The IP address of this connection can be located within the system software in __Settings__ > __Network__ > __View Connection Status__. This is the address you need to use to connect to the Unity Profiler.

It is also important to note that while internet, PSN and Unity Profiler functionality is available over WiFi, the volume of Profiler information being sent can overwhelm a wireless connection. For maximum stability, use two wired connections if you wish to use the Unity Profiler.

If you can’t make a connection, carry out the following checks:

* Make sure the host PC and both network connections on the devkit are all on the same subnet. See [Wikipedia: Subnetworks](https://en.wikipedia.org/wiki/Subnetwork) to get started if you are not familiar with subnets.

* Ensure that Unity Editor is not blocked by any firewall software on your computer.

* Check your router or access point settings to make sure multicast packets are allowed between networked devices (no WiFi peer isolation enabled). If you don’t know how to do this, check the documentation for your router or access point.

* Run your build on the PS4 and check the [Console Output](https://ps4.scedev.net/resources/documents/SDK/latest/Console_Output-Users_Guide/0002.html) ([https://ps4.scedev.net](https://ps4.scedev.net)) for any output regarding player connection.

* Verify that the IP address can be reached from the host PC, for example using [Ping ](https://technet.microsoft.com/en-us/library/bb490968.aspx)in the command line. Remember that Unity profiler uses the PS4 LAN connection (rather than the DEV connection), so you need to check with the IP address found in __Settings__ > __Network__ > __View Connection Status__.

If you still can’t make a connection, try installing and running [Wireshark](https://www.wireshark.org), a third-party network protocol analyzer. To configure Wireshark to display the announcement packets being sent from the PS4, run it on your PC with a filter of `ip.addr eq 225.0.0.222`. See [Wireshark’s software documentation](https://www.wireshark.org/docs/) for more information on how to do this.