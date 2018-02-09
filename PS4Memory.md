# PlayStation 4 memory

The PlayStation 4 system uses a single block of memory shared between the CPU and the GPU. The memory can be accessed using different access paths called __Onion__ and __Garlic__. See Sony’s documentation on [PS4 ](https://ps4.scedev.net/resources/documents/SDK/latest/Memory_System_Performance/__document_toc.html)[SDK memory system performance](https://ps4.scedev.net/resources/documents/SDK/latest/Memory_System_Performance/__document_toc.html) for details.

| | **Base console** | **PS4 Pro (Neo) mode console** |
|:---|:---|:---|
| **Total system memory**| 8GB | 8GB, plus the OS reserve |
| **Total memory available** <br/>See (1), below | 4,608MB | 5,120MB |
| __Garlic__ **memory** <br/>See (2), below | Garlic heap size | Garlic heap size, plus 512MB |
| __Onion__ **memory** <br/>See (3), below | Total memory available, minus the Garlic memory | Total memory available, minus the Garlic memory|


1. **Total memory available** is the memory available to a game after Unity player and OS allocations are taken into account. There is a 448MB default flexible memory allocation for loading code (including the Unity Player) and plugins.

2. **Garlic memory** is controlled by the __Player Settings__ > __Garlic Heap Size__ in Unity (with an additional 512MB when running Neo mode).

3. **Onion memory** is the remainder of total memory available after allocating Garlic memory.

The Unity player allocates memory to either the Garlic or Onion access path, according to the following rules:

* All Mesh and Texture data is stored in Garlic memory. 

* All other memory allocations are made in Onion memory. 

* Textures are first loaded into Onion memory, then copied to Garlic memory.

* If a Texture is marked as read/write, it remains in both Onion memory and Garlic memory.

* If a Texture is read-only, the Onion memory used to allocate it is made available for reuse.

## Onion and Garlic in the Memory Analyzer

When using the PlayStation 4 Memory Analyzer (see Sony PS4 documentation on the [Memory Analyzer](https://ps4.scedev.net/resources/documents/SDK/latest/Memory_Analyzer-Users_Guide/__document_toc.html)), Garlic allocations are in the `ALLOC_GFX` group (in yellow) and Onion allocations are in the `onion_sys_allocator` groups (in orange).

# Memory Budget Mode

The PlayStation 4 development hardware (DevKit) has a debug setting called __Memory Budget Mode__. The default setting is __NORMAL__. Set __Memory Budget Mode__ to __LARGE__ to allow the use of additional memory that isn’t available on retail PlayStation 4 hardware. The Unity Profiler has a memory overhead itself, so this mode is useful when profiling a game that is already using most of the memory available. See Sony’s PS4 documentation on [Memory Budget Mode](https://ps4.scedev.net/resources/documents/SDK/latest/Programming-Startup_Guide/0006.html#__document_toc_00000033) to learn more.

To make sure you are not using more memory than your game has available, it is recommended that you only set __Memory Budget Mode__ to __LARGE__ when necessary for specific uses, and set it back to __NORMAL__ as soon as possible afterwards.

**Note:** Memory Budget Mode is not available on TestKit hardware.
