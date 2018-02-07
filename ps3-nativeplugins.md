PlayStation3: Native Plugins
============================


This page describes [Native Code Plugins](Plugins) for PS3


Plugin development:
-------------------



* The PRX should be written according to SCE's Specifications. Please consult Lv2_PRX-Programming_Guide located in the pdf SDK docs under development_basic.

Plugin requirements:
--------------------


* Linked against the same SDK as Unity. (See the [Getting Started](ps3-gettingstarted) page for current SDK Version.)
* OnModuleStart / OnModuleStop functions have the following signature:

`int OnModuleStart(unsigned int args, void* argp);`

`int OnModuleStop(unsigned int args, void* argp);`



* The name used for [DllImport] in the script should be identical to the name used for `SYS_MODULE_INFO` and `SYS_LIB_DECLARE`

`[DllImport("MyPlugin")]` will load the plugin that has been declared with `SYS_MODULE_INFO(MyPlugin, ... )` and `SYS_LIB_DECLARE(MyModule, SYS_LIB_AUTO_EXPORT)`;



* In order to be loaded by the runtime, the plugin's .sprx and _stub.a and must reside in _/path/to/project/Assets/Plugins/PS3/_. For example if your plugin is called _MyPlugin_, then _/path/to/project/Assets/Plugins/PS3/_ should contain _MyPlugin.sprx_ and _MyPlugin_stub.a_
    * See [Project Structure](ps3-projectstructure) for more details
    * See [Mono Interop docs](http://www.mono-project.com/Interop_with_Native_Libraries) for marshaling details.


Notes
-----



* The name used to identify the module (SYS_MODULE_INFO/SYS_LIB_DECLARE) must be maximum 25 characters.
* A PrxPluginArgs structure is passed as argp into the OnModuleStart function. This structure is defined as: 

````
struct PrxPluginArgs
{
	PrxPluginArgs() : m_Size(o) ,m_Version(o) {}
	static const uint32_t s_Version = 0x0102;
	uint32_t m_Size;
	uint32_t m_Version;
	const void* m_NpCommunicationId;   // Cast to SceNpCommunicationId* if used by plugin (defined as void* to avoid all native plugins requiring NP header file inclusion)
	const void* m_NpCommunicationSignature;  // Cast to SceNpCommunicationSignature*
	const void* m_NpCommunicationPassphrase; // Cast to SceNpCommunicationPassphrase*
	bool m_NpHasTrophyPack;
	const char* m_NpServiceID;
	const char* m_TitleID;
	int m_NpAgeRating;
	bool m_Trial;
	void* m_SpursInstance;
	bool m_bDevelopment; // Introduced in 0x0102 onwards
};
````

If required, the native plugin can then access elements of this structure as follows, using the SPURS instance handle as an example:

````
PrxPluginArgs AppInfo;

AppInfo = *(PrxPluginArgs*)argp;

gSpursInstance = (CellSpurs2*)AppInfo.m_SpursInstance;
````



Example Plugin using ProDG's VSI.NET for Visual Studio 2008
-----------------------------------------------------------


1. Create a new Project in Visual Studio.

    * Select the PS3 PPU PRX template.
    * Make sure that in the post build events “make_fself_npdrm” is used instead of the default “make_fself”.

2. Build the Project.

3. Copy the generated Plugin files to your Unity Project folder.

    * It must be placed at this location:

        * Assets/Plugins/PS3/XXXXXXX.sprx
        * Assets/Plugins/PS3/XXXXXXX_stub.a

4. Use the plugin in your script code :

    * Include InteropServices : using System.Runtime.InteropServices;
    * Declare the dll with dllimport : [DllImport ("Name Of The Module")]
    * Use preprocessor defines to compile your code for PS3 only.

````
using UnityEngine;
using System.Runtime.InteropServices;
		
public class UseThePlugin : MonoBehaviour {

   if UNITY\_PS3 && !UNITY\_EDITOR
	[DllImport ("Unity_PRX_Example")]
	private static extern int _Unity_PRX_Example_export_function ();

	void OnGUI () {
		GUILayout.Label ("Return value: " + _Unity_Example_export_function().ToString());
	}

   else
	void OnGUI () {
		GUILayout.Label ("Run the Test on the PS3");
	}	

   endif
}
````

5. Verify it works

    * The default PS3 PPU PRX project returns a zero. If that worked you should see "Return value: 0" printed on the screen.


Reference documentation
-----------------------


* PRX files - https://ps3.scedev.net/docs/ps3-en,Lv2\_PRX-Programming_Guide/1/


* PRXS files - https://ps3.scedev.net/docs/ps3-en,Application\_Requirements,Executable_Files/1/


* NPDRM - https://ps3.scedev.net/docs/ps3-en,NP\_DRM-Package_Requirements,Introduction/


* PRX commands - https://ps3.scedev.net/docs/ps3-en,Lv2\_PRX-Programming_Guide,Commands_Reference/1/


* StdLibs for PRXS plugins - https://ps3.scedev.net/docs/ps3-en,C\_and\_Cpp\_standard\_libraries,C\_and\_Cpp\_standard\_libraries\_1/1
