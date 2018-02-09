Using Plugins for WiiU
==========

You can find basic native plugin examples by importing a Unity Package by selecting Assets -&gt; Import Package -&gt; Wii U - Plugin Examples.

The package includes the following plugins:

* Account System - getting account status.
* Friend Presence - getting status of friends.
* OLV - contributing to Miiverse.
* Spot Pass - sample for SpotPass plugin.

------
Unity provides a minimal interface for a plugin to communicate with it. Interface declarations can be imported by including `UnityInterface.h` file which you will find in imported package.

Compiled plugin files (rpl) must be placed into `Assets/Plugins/WiiU` folder. During player build Unity will scan this folder and copy rpl files next to the main executable as required by the OS.

It is advisable to review compiler flags that are specified in build.cmd if you keep using it to build shippable plugins.

![](../uploads/Main/Plugins_01.png) 

When defined, the following global functions will be called right after the plugin is loaded.

````
extern "C" int rpl_entry(void * handle, int reason);
````
`rpl_entry` is the first function that is called and it is done by the dynamic linker.

````
extern "C" void UnityManageMemory (DotNetCoAllocFunc* coAlloc, DotNetCoFreeFunc* coFree);
````
This callback provides access to memory management facilities. The function pointers represent functions that may be called to allocate/deallocate memory. For example when returning a string, a `char*` buffer needs to be allocated using `coAlloc` function.

````
extern "C" void UnitySetGraphicsDevice (void* device, int deviceType, int eventType);
extern "C" void UnityRenderEvent (int eventID);
````
Graphics device callbacks as described in [Native Plugin Interface](NativePluginInterface) section.



##Type Marshaling
For information on type marshaling, please refer to [Interop with Native Libraries](http://www.mono-project.com/docs/advanced/pinvoke/#marshaling) section in mono documentation.

