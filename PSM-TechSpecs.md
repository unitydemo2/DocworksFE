PSM Technical Specifications
====

Main purpose of this document is to explain the differences between Unity for PSM compared to other Unity running on other platforms (such as PC or Mac, or mobiles like iOS and Android).

It also briefly outlines the hardware specifications of the PS Vita - the platform on which Unity for PSM runs.

## Unity for PlayStation&#174;Mobile

Unity for PSM is a runtime and development tools suite for the PlayStation&#174;Mobile platform/business model. It is distinctively separate from the pre-existing "PSM SDK" - "PSM SDK" and "Unity for PSM" do not share tools or APIs.  Because of this, "PSM SDK" and "Unity for PSM" features cannot be used together, and cannot co-exist within the same PSM application.

### Runtime
The Unity for PSM runtime targets the PlayStation&#174;Vita hardware specifically. Application code runs in a Mono ['sandboxed'](http://en.wikipedia.org/wiki/Sandbox_(computer_security)) environment where only managed (C# / UnityScript / Boo) code is allowed. 
This means that native plugins are not supported with Unity for PSM, and that only of the PS Vita native APIs exposed through the Unity for PSM script API (UnityEngine.PSM.*) are available. 
The Mono runtime uses Just-In-Time (JIT) compilation of application (user) scripts.

### Rendering
Unity for PSM reuses the same graphics driver used in the "Unity PS Vita".
This ensures that a high-performance rendering path is available also with Unity for PSM.
But the graphics driver behaves quite differently in one key aspect : 
A shader instance is only compiled when it is actually used - that is right before rendering the material from which it is referenced.
This means that the classic ``fallback shader`` mechanism provided in Unity is not available on PSM. An unsupported shader (a shader with a programming error, or otherwise fails to compile) will simply be replaced with the Default Shader, which usually produces a pink color output (and the compilation error output written to the device log).
And because this step can sometimes be computationally intensive, shaders already compiled are cached, and can be reused on subsequent application runs (provided the shader hasn't changed).
One benefit of compiling shaders at runtime is that Unity for PSM also supports the older Unity "fixed function" shaders. 



## PlayStation&#174;Vita

Unity for PSM currently only runs on the PS Vita.

## CPU
The CPU has 3 hardware threads available to the application. Unity uses at least 2 (main and rendering), so creating more than one additional worker thread from managed code is not likely to yield any additional benefit. 
But this of course depends on how the application itself is behaving. For example,  a GPU-limited application might have plenty of CPU time to spare.

### Graphics
PowerVR-based graphics core. Shaders are written in Cg. Textures are compressed using DXT or PVRTC (PVRTC is currently not supported by Unity).
Screen resolution is 960 &#215; 544.

### Memory
The physical memory available in the PS Vita is 256MB of system memory, and 128MB of video memory. 
Not all of this is available to a "Unity for PSM" application - below is a breakdown of how much is reserved, for what, and how much is available to the application.

|**_System Memory:_** ||
|:---|:---|
|Physical Memory | 256 MB|
|Reserved | -8 MB|
|_Available to "Unity for PSM"_ | _248 MB_|
|"Unity for PSM" executable | -32 MB|
|Buffers (sub-system allocations) | -32 MB|
|**Available to App** | **184 MB**|

_Table 1. System memory with "Unity for PSM"_

|**_Video Memory:_** ||
|:---|:---|
|Physical Memory | 128 MB|
|Reserved | -16 MB|
|_Available to "Unity for PSM"_ | _112 MB_|
|Buffers (screen and commands) | -25 MB|
|**Available to App** | **87 MB**|

_Table 2. Video memory with "Unity for PSM"_

The numbers above are theoretical limits. It's good practice to allow for a few MB of unused buffer space, to not run out of memory while running the application.
The memory listed as "Available to App" is used not only for scripts, but also for any kind of additional game data, such as meshes, physics/collision structures, etc.

### Input / Output
The PS Vita has these input / sensor capabilities, all which are available from a "Unity for PSM" application

* Directional input and &#215; &#9675; &#9633; &#9651; buttons (digital)
* Left and right shoulder buttons (digital)
* Left and right analog sticks (x/y axis)
* On-screen touch input + rear touch pad
* Compass / Gyro / Accelerometer / Location
* Front and rear camera
* Speaker and microphone

