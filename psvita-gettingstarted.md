PS Vita Getting Started
===

##Developing for PS Vita
To develop for the Vita you must be a Sony registered developer and own the appropriate hardware. See the PS Vita Setup or PS Vita Setup for Source Licensees page depending on your license for a seat setup checklist.

##Build Information
The required SDK version is specified in the release notes of each respective PS Vita Add-on/Unity build.

##Access PS Vita Unique Functionality
Unity PS Vita provides a number of new scripting APIs to access PSN services, input, native video support and much more. See the UnityEngine.PSVita namespace in the scripting API.

##How Unity Vita differs from Desktop Unity

* Strongly Typed JavaScript
	* Dynamic typing in JavaScript is always turned off in Unity PS Vita. This is the same as adding `#pragma strict` to your scripts, but it is done by default instead. This greatly improves performance. When you launch an existing Unity Project, you will receive compiler errors if you are using dynamic typing. You can easily fix them by either using static typing for the variables that are causing errors or taking advantage of type interface
* Ahead-Of-Time compilation
	* Scripts are AOT compiled into a static library which is subsequently linked with the Unity Run-Time to produce the player. Due to platform limitations, JITing is not supported. This means that reflection cannot be used
* Limited memory
	* The console has a total of 256MB of System (Main) Memory and 128MB of Video Memory. The Unity Player and AOT'd Script Assemblies will take away from the main memory, also the PS VIta system software uses some of this memory. It is important to note that development consoles have 512MB of memory so fitting in memory on a development console is no guarantee that your application will work on the a retail console.
* Limited  MSAA Support
	* Unity for PS Vita supports hardware MSAA with 2 or 4 samples for the main render target and render target textures.
* Video formats
	* Unity supports the MPEG-4 AVC/H.264 standard format. For more information see the documentation at [https://psvita.scedev.net/docs/vita-en,Encoding-Users_Guide-vita,Overview/1/](https://psvita.scedev.net/docs/vita-en,Encoding-Users_Guide-vita,Overview/1/)



