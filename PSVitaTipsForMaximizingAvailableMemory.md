PS Vita Tips for Maximizing Available Memory
====

### Dev kit vs Test/Retail kit and Avoiding The Crunch-Time Blues

The last thing you want to happen when you are about to submit your game is to suddenly find out that it doesn’t fit into memory on a retail PS Vita. A retail/test kit has roughly half the amount of memory that a dev-kit has. During development you should regularly switch your dev-kit to mimic retail memory to check that you are fitting in memory. To do this open the PS Vita target settings tool which is accessible from "Neighbourhood for Playstation®Vita", go to the "Boot Parameters" section and change "Memory Size" to "Console Size".

### Using the  Physical Contiguous Memory Area

The Vita has a 26MB area of specialised memory set aside for decoding FMV, if your game does not play FMV or only plays it once, i.e. during game boot up, then you can release this memory and make it available for general allocations. To do this call one of the following functions as soon as the game boots or after playing any intro FMV…

````
UnityEngine.PSVita.PSVitaVideoPlayer.TransferMemToHeap()
````

This makes the 26MB of physical contiguous memory available for general heap allocations.

````
UnityEngine.PSVita.PSVitaVideoPlayer.TransferMemToMonoHeap()
````

This makes the 26MB of physical contiguous memory available for general Mono heap allocations.

Note: You should only call one of these functions, and only call it once, after calling either of them it is no longer possible to play FMV.

### Making Better Use Of cdram (VRAM)

By default all mesh data is allocated in main system memory and all available cdram is reserved for textures and render targets. If your game does not use all of cdram for textures and render targets then you can tell Unity to allocate mesh data in cdram, this is done from the editor, go to ``Player Settings &gt; Other Settings &gt; Mesh Video Mem`` and set it to the number of MB of VRAM that you would like to reserve for mesh data. Once this is setup mesh data will be allocated in cdram until the area set aside for mesh data becomes full, then allocations revert back to main system memory.

### Texture Size

It is common practice to tell unity to half or quarter texture sizes for PS Vita especially in cross-platform games where higher resolution textures may be required on other platforms. Care must be taken as this option only has any effect when textures have mip-maps generated as scaling is achieved by skipping mip-levels.

Avoid using non-power of two (NPOT) sized textures where possible, if you do need to use NPOT textures make sure to use an un-compressed texture format. The PS Vita cannot render directly from an NPOT compressed texture so a copy is made into a larger power of two (POT) texture which is very wasteful of memory. If NPOT textures are required then it is more memory efficient to use an uncompressed format such as 16 bit RGBA.

### Mono Heap Behaviour

It is possible to tweak the way the mono heap behaves, by default it grows by a percentage of the current size when it needs to reserve more memory from the system, typically this is ok but can be wasteful if your scripts allocate a lot of mono memory. You can use the following method to adjust this behaviour:

````
UnityEngine.PSVita.Utility.SetMonoHeapBehaviours(bool constrain, bool tight)
````

* ``Setting tight = true`` causes the heap to only grow by the exact amount needed.

* ``Setting constrain = true`` causes the heap to grow by a constant 8MB when it needs to reserve more memory but only if tight = false.

NOTE that setting either of these to true can result in more frequent garbage collection so they may not be appropriate for your game, but they can be worth a try.

### Memory HUD

Finally, there is a diagnostic HUD that you can turn on for development builds that displays low-level information on memory usage which you might find useful, just do the following in your scripts to enable the memory HUD.

````
UnityEngine.PSVita.Diagnostics.enableHUD = true;
````

### Memory Expansion Mode

The memory size of the main memory's physical memory to be used by the application can be expanded by setting a Memory Mode. 

Available modes include:

* 29MiB - Only this app can be run.
* 77MiB - Only this app can be run, the internet browser cannot be used.
* 109MiB - Only this app can be run, the internet browser and title store cannot be used.

The option for Memory Expansion Mode is available in the player settings in the Param File section.

This setting cannot be changed dynamically.

Detailed informaiton on Memory Expansion Mode can be found in the SDK documentation at [https://psvita.scedev.net/docs/vita-en,Programming-Startup_Guide-vita,Resources_that_Can_Be_Used_by_an_Application/1/](https://psvita.scedev.net/docs/vita-en,Programming-Startup_Guide-vita,Resources_that_Can_Be_Used_by_an_Application/1/)