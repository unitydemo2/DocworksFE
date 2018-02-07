# PS4 Troubleshooting

## Log files

If your PS4 application is crashing, the first thing you need to do is to check your application log. You can read the log while your application is running using the Console Output application from the PS4 SDK. 

Running out of memory is one of the most common causes of crashes. To diagnose it, you can search the log for messages about failed memory allocations. Here’s an example of how it could look in your log:

```
fps 52.152 (19.175 ms), objects: 263, coroutines: 0
sceKernelAllocateDirectMemory failed with 0x80020023
sceKernelAllocateDirectMemory failed with 0x80020023
DynamicHeapAllocator allocation probe 1 failed - Could not get memory for large allocation 4016779264.
sceKernelAllocateDirectMemory failed with 0x80020023
sceKernelAllocateDirectMemory failed with 0x80020023
DynamicHeapAllocator allocation probe 2 failed - Could not get memory for large allocation 4016779264.
sceKernelAllocateDirectMemory failed with 0x80020023
sceKernelAllocateDirectMemory failed with 0x80020023
DynamicHeapAllocator allocation probe 3 failed - Could not get memory for large allocation 4016779264.
sceKernelAllocateDirectMemory failed with 0x80020023
sceKernelAllocateDirectMemory failed with 0x80020023
DynamicHeapAllocator allocation probe 4 failed - Could not get memory for large allocation 4016779264.
sceKernelAllocateDirectMemory failed with 0x80020023
sceKernelAllocateDirectMemory failed with 0x80020023
DynamicHeapAllocator out of memory - Could not get memory for large allocation 4016779264!
Could not allocate memory: System out of memory!
Trying to allocate: 4016779264B with 4096 alignment. MemoryLabel: Mono
Allocation happend at: Line:407 in C:/buildslave/unity/build/PlatformDependent/PS4/Source/Allocator/PS4Memory.cpp
Memory overview

[ ALLOC_DEFAULT ] used: 8100027132B | peak: 0B | reserved: 8108553212B 
[ ALLOC_TEMP_JOB ] used: 0B | peak: 0B | reserved: 2097152B 
[ ALLOC_PROFILER ] used: 628000B | peak: 628000B | reserved: 33554432B 
[ ALLOC_GFX ] used: 0B | peak: 149626568B | reserved: 0B 
[ ALLOC_TEMP_THREAD ] used: 32768B | peak: 0B | reserved: 3670016B 
Could not allocate memory: System out of memory!
Trying to allocate: 4016779264B with 4096 alignment. MemoryLabel: Mono
Allocation happend at: Line:407 in C:/buildslave/unity/build/PlatformDependent/PS4/Source/Allocator/PS4Memory.cpp
```

For more information on PS4 memory allocation, refer to [PlayStation 4 memory](Manual/PS4Memory.html).

## Core dumps

If the log doesn’t give you enough clues, you can examine the PS4 core dump. Core dumps are a feature of the PS4 system that are available in DevKits and TestKits, even in Release Mode. They are used during development, but can also be retrieved from Sony’s servers after a title has been released. Make sure to read the [Core Dump Documentation](https://ps4.siedev.net/resources/documents/SDK/4.500/Core_Dump_System-Overview/0003.html#__document_toc_00000002) for all the details.

### Generating core dumps
First, you need to set up your DevKit to generate a core dump in case of a crash. To do this, select Debug Settings > Core Dump > Core Dump Mode and set it to coredump. After setting this option, the system will automatically generate a core dump the next time your application crashes.

### Accessing core dump files
The generated files are stored in the DevKit HDD, in a folder for each generated dump. The folder will have the following naming convention:

```
/data/sce_coredumps/<title ID>_<timestamp>
```

If you connect to the DevKit using the Neighborhood for PlayStation 4 application, you should be able to see the files in a file explorer, in a folder similar to:

```
O:\192.168.1.192\data\sce_coredumps\CUSA05885_1486154714
```

### Loading the core dump
Within the core dump generated files, you should find one with the extension .orbisdmp. You can use Visual Studio to load this file and examine its contents. You will need to install the respective Visual Studio Integration provided by SIE, via the SDK Manager. 

If you are unable to load the dump file in Visual Studio, try the following:

* If you have multiple versions of Visual Studio installed, make sure the Integration tools are installed in the one you are using to open the dump file. 
* Run your SDK Manager and check that __SDK Development Tools__ > __Tools for Development__ > __Debugger X.XX and Visual Studio 20XX Integration__ are installed. 
* You can also check __Help__ > __About__ in Visual Studio to see which products are installed.

After loading the file, use the __Start debugging__ option in the __Actions__ section of the loaded page to see the crashed Call Stack, Thread information, Kernel Objects, Output Window (log) and more.

### Adding debug symbols to the Call Stack

The Call Stack window in Visual Studio doesn’t have [debug symbols](https://en.wikipedia.org/wiki/Debug_symbol) loaded by default. You’ll see memory addresses instead of function names, which makes it hard to find clues. To add symbols to your Call Stack and be able to see function names, you can use the __Set Symbol Path__ option in Visual Studio, located in the __Actions__ section of the loaded dump page.

The following image shows an example of a Call Stack without symbols (left) and the same Call Stack after loading symbols (right). 

![](../uploads/Main/PS4CallStack.png)

The Call Stack also shows the names of the PS4 modules containing the called code. The following modules produced by Unity contain debug symbols in the .bin/.prx file itself. You need to add the folder containing the files to the symbol path list in Visual Studio:

|:---|:---|:---|
|Module Name| Used with scripting backend|Project specific|
|eboot.bin|Both|No|
|mono-ps4.prx|Mono2x|No|
|MonoAssembliesPS4.prx|Mono2x|Yes|
|PS4Util.prx|IL2CPP|No|
|Il2CppUserAssemblies.prx|IL2CPP|Yes|


Project-specific modules contain your script code. They change every time you build your project. For that reason, you need to get the exact version of the file that was included in the build that crashed, to be able to add symbols.

Non-project specific modules are included in your Unity installation and don’t change between builds or between projects, they only change between Unity versions.

#### Symbol folders for a PC-hosted build
* The __eboot.bin__ module is placed in the selected build folder. 
* Other modules are placed in (build folder)\Media\Modules.

#### Symbol folders for a package/ISO build
* The __eboot.bin__ module is placed in the (project folder)\Temp\StagingArea folder. 
* Other modules are placed in (project folder)\Temp\StagingArea\Data\Modules.

Be aware that the complete (project folder)\Temp\ folder is always deleted as soon as you close the Unity Editor.

#### Alternative symbol folders for non-project specific modules
Alternatively, non-project specific modules (eboot.bin, PS4Util.prx, mono-ps4.prx) can be found in your Unity installation folder. This is handy if you’ve already lost the files used in your crashed build, but your project-specific symbols will be missing. Make sure you use the files from the correct version of Unity.

* The __eboot.bin__ module is located at: 
```
(Unity Install Folder)\Editor\Data\PlaybackEngines\PS4Player
```(note that it’s not named __eboot.bin__, but it’s one of the .self files in this folder.) 


* Other modules are placed in 
```
(Unity Install Folder)\Editor\Data\PlaybackEngines\PS4Player\Data\Modules
```

### Generating a core dump without a crash
Sometimes it is useful to generate a core dump even if the application has not crashed. A common case would be when the application hangs. 

You can generate a core dump while an application is running by using the “★Generate Core file” option in the [Development Support Features by Application](https://ps4.siedev.net/resources/documents/SDK/4.500/System_Software-Overview/0005.html) menu. 

Alternatively, you can use the orbis-ctrl pdump command line tool in an elevated command prompt window with the following line:

```
orbis-ctrl pdump processname pathwherethefilewillbesaved mini
```

You can get the process name via Neighborhood for PlayStation 4 in the process list displayed by selecting your DevKit and then right clicking and selecting __Kill process__. In test environments, the process name is usually project-specific symbols.

## Reporting a crash issue to Unity
If you can’t get enough clues to fix the problem by yourself, you can send your core dump files to us. You can [file a new bug report](https://unity3d.com/unity/qa/bug-reporting), or ask for help on the [Unity forum for PS4 in Devnet](https://ps4.siedev.net/forums/forum/29/). Please attach the complete core dump folder and tell us what version of Unity you are using.

Additionally, if the Call Stack touches your script code module (MonoAssembliesPS4.prx or Il2CppUserAssemblies.prx), please make sure to also attach that file too.

To make sure we get as much information as possible from the core dump, you can set your DevKit to generate a __Full Dump__ instead of the default __Mini Dump__. You can set it in __Debug Settings__ > __Core Dump__ > __Dump Level__.

If you prefer to post just a Call Stack (not an entire core dump) on our support channels, please make sure you add debug symbols to it first. Attaching your entire log file is also a good idea.

---
* <span class="page-edit">2017-08-30  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">New feature in Unity 2017.1</span>
