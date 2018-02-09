Windows Debugging
=================

Unity provides some facilities to ease the debugging on Windows for forensic or live debugging of game or editor processes.

### Native vs. Managed Debugging
First, clarity regarding debugging. There are two types of debugging that need addressing within Unity. There is the native C++ debugging as well as the C# managed debugging. For platforms supporting IL2CPP, there will be only native debugging, but managed debugging will stay for the editor for fast iteration purposes.

#### Native Debugging
Native Debugging is facilitated by having symbols (pdb files) for the associated binary files (exe or dll).

#### Managed Debugging
On Windows, the standard .NET managed symbols are stored in pdb files as well, however when using mono, there are mdb files.

### Symbols
Unity provides a symbol store at http://symbolserver.unity3d.com/ . This server URL can be utilized in windbg or VS2012 and later for automatic symbol resolution and downloading (much like Microsoft's symbol store). 

#### Windbg Setup
The easy way to add a symbol store on windbg is the .sympath command.  
> `.sympath+ SRV*c:\symbols-cache*http://symbolserver.unity3d.com/`  

Let's break that down:

> `.sympath+`  
The + addition, leaves the existing symbol path alone, and appends this symbol store lookup

> `SRV*c:\symbols-cache`  
The SRV indicates a remote server to fetch from, while the c:\symbols is a local path to cache the downloaded symbols and to look there first before downloading again.

> `*http://symbolserver.unity3d.com/`  
The path to the symbol store to fetch from

#### Visual Studio Setup
**Note:** VS2010 and earlier do not function with http server symbol stores.  
1. Go to Tools -> Options  
2. Expand the Debugging Section, select Symbols  
3. Specify a cache directory (if not already specified)  
4. Add a "Symbol file (.pdb) location" of http://symbolserver.unity3d.com/
 
### Live Debugging
Live Debugging is the scenario of attaching a debugger to a process that is running normally, or to a process where an exception that has been caught. In order for the debugger to know what's going on, the symbols need to be included in the build. That's what the steps above should address. The one additional thing to know is that the game executable is named according to your game name, so the debugger may have issues finding the correct pdb if it doesn't have access to your renamed executable.


#### Setting up automatic exception debugging
On Windows, Microsoft sets up automatically on application crashes to go to Dr Watson/Error Reporting to Microsoft. However, if you have Visual Studio or windbg installed, Microsoft provides a facility to savvy developers to instead opt to [debug the crashes](https://msdn.microsoft.com/en-us/library/windows/desktop/bb204634(v=vs.85).aspx).  
For ease of installing, here's a registry file contents to install:  

    Windows Registry Editor Version 5.00
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug]
    "Auto"="1"
    [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug]
     "Auto"="1"

A little extra for editor debugging:
> `Unity.exe -dbgbreak`  
Will launch Unity and immediately offer a debugger to connect if the automatic crash handling is set up

### Post-Mortem/Forensic Debugging
Windows provides facilities to investigate crash dump files (.dmp or .mdmp). Depending on the type of crash dump, there may simply be stack information or perhaps the entire process memory. Depending on the contents, various possibilities exist in seeing what may have happened to cause a crash. In the usual case, you often at least have a stack to investigate (if it's a valid stack...)

To investigate a dump file, your options are to load up via Visual Studio or windbg. While Visual Studio is a more friendly tool to use, its power is a bit more limited than windbg.

### Debugging Hints and Tricks

#### Managed exceptions in native land
A NullReferenceException will often look like this:

 	    1b45558c()	
    >	mono.dll!malloc(unsigned int size=12)  Line 163 + 0x5f bytes	C  
 	    mono.dll!g_hash_table_insert_replace(_GHashTable * hash=0x065c3960, void * key=0x0018cba4, void * value=0x0018cb8c, int replace=457528232)  Line 204 + 0x7 bytes	C  
     	mono.dll!mono_jit_runtime_invoke(_MonoMethod * method=0x242bf8b0, void * obj=0x065c3960, void ** params=0x0018cba4, MonoObject * * exc=0x0018cb8c)  Line 4889 + 0xc bytes	C  
This is not a crash in malloc, nor in mono - it's a NullReferenceException that's either:  
* Caught by the VS debugger
* Unhandled in a user's player, causing the player to exit

#### Viewing managed stack frames

With the previous example again:  

 	    1b45558c()	
    >	mono.dll!malloc(unsigned int size=12)  Line 163 + 0x5f bytes	C  
 	    mono.dll!g_hash_table_insert_replace(_GHashTable * hash=0x065c3960, void * key=0x0018cba4, void * value=0x0018cb8c, int replace=457528232)  Line 204 + 0x7 bytes	C  
     	mono.dll!mono_jit_runtime_invoke(_MonoMethod * method=0x242bf8b0, void * obj=0x065c3960, void ** params=0x0018cba4, MonoObject * * exc=0x0018cb8c)  Line 4889 + 0xc bytes	C  

The lines without any information are managed frames. There is, however, a way to get the managed stack information: mono has a builtin function called mono_pmip, which accepts the address of a stack frame and returns a char* with information. You can invoke mono_pmip in the Visual Studio immediate window:

> `?(char*)mono.dll!mono_pmip((void*)0x1b45558c)`  
0x26a296c0 " Tiles:OnPostRender () + 0x1e4 (1B4553A8 1B4555DC) [065C6BD0 - Unity Child Domain]"`

**Note:** This only works where mono.dll symbols are properly loaded.

#### Force Applications to Create Dumps

Sometimes there are cases where the application doesn't crash with the debugger attached, or an application crashes on a remote device where the debugger is not available. However, you can still get useful information if you can get the dump file - follow the below steps in order to do so.

**Note:** These instructions are for Windows Standalone, Windows Store Apps and Windows Universal Apps (when running on desktop).

* Open the registry.
* Navigate to HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting
* Create LocalDumps folder if it's not there.
* Add following keys:
    * "DumpFolder"=&lt;FolderPath goes here&gt; , for example, C:\Temp
    * "DumpCount"=dword:00000010
    * "DumpType"=dword:00000002
* Launch the application (it can be anything that runs on Windows - Windows Store App or Windows Standalone Executable)
* Reproduce the crash, the dump file should be created in your specified folder. You can either open the dump file with Visual Studio or WinDbg.

