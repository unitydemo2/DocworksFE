Profiling with Unity Profiler
=====

Currently Unity supports Scripting and Graphics profiling.

To connect profiler you will need to do following steps:

1. Setup your Wii U Internet connection by going to devkit settings. This must be the Wii U's network connection, not the MION.
1. Make sure that your PC and devkit are connected on the same network.
1. Select **Build Type: Development** in [Build Settings](wiiu-buildsettings), check **Autoconnect Profiler**, press build and launch the application on the devkit.
1. After your application starts, go to open Unity Profiler by selecting Window-&gt;Profiler.
1. In Active Profiler field make sure that your devkit is selected (enter IP address if necessary).
1. After few seconds your profiler will be connected and you will receive all the data in the Profiler view.

We also encourage to use Ethernet connection with the devkit when profiling (using a USB-Ethernet adapter). Data may be missed or the profiling feel sluggish if using Wifi connection.

