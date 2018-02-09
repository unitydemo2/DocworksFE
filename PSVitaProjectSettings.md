PS Vita Project Settings
===

Unity for PSVita comes with additional project settings.

Build Settings: General

* Build Type

Player Settings:

* Icon
* Splash Image
* Other Settings

Player Settings: Publishing Settings

* Default Live Area
* Custom Live Area
* Software Manual
* Package Parameters
* Digital Rights Management
* Media Type & Size
* Playstation(R)Network

----

##Build Settings
###Build Type
**PC Hosted**

* Creates a package to be launched from the PC.
* Option to link with development player (for player connection, profiler and full TTY output).
* Autoconnect Profiler option.
* Explicit Null Checks option to enable reporting of  null references in the TTY.

**PSVita Package**

* Creates a package to be launched on the target device.
* Option to link with development player ( for player connection, profiler and full TTY output).
* Submission Materials option (only available if 'Development Build' is NOT enabled). Outputs materials required when submitting a package to SCE.
* Autoconnect Profiler option (only available if 'Development Build' is enabled).
* Explicit Null Checks option to enable reporting of null references in the TTY.

##Player Settings
###Icon 
The Icon (Override for PSP2) option should be ticked in order to add a Still Image icon. This icon is used on the PSVita Home screen.

_Image Format_

* 128x128 pixels in size
* PNG

More information on the Still Image Icon can be found at [https://psvita.scedev.net/docs/vita-en,Content_Information-Specifications-vita,Still_Image_Icon/1/](https://psvita.scedev.net/docs/vita-en,Content_Information-Specifications-vita,Still_Image_Icon/1/).

###Splash Image
The Splash Image or Start-up Image will immediately display when the gate is tapped from LiveArea.

_Image Format_

* 940x544 pixels in size
* PNG

More information on the Start-up image can be found at [https://psvita.scedev.net/docs/vita-en,Content_Information-Specifications-vita,Start-up_Image/1/](https://psvita.scedev.net/docs/vita-en,Content_Information-Specifications-vita,Start-up_Image/1/)

###Other Settings
**Rendering**

_Static Batching_

* Static batching allows the engine to reduce draw calls for geometry of any size (provided it does not move and shares the same material). Static batching is significantly more efficient than dynamic batching. You should choose static batching as it will require less CPU power.

_Dynamic Batching_

* Unity can automatically batch moving objects into the same draw call if they share the same material and fulfill other criteria. Dynamic batching is done automatically and does not require any additional effort on your side.

The benefits of static and dynamic batching can vary greatly from game to game. General information and tips on using Static and Dynamic batching is available [here](DrawCallBatching).

_GPU Skinning_

* Uses SX11/ES3 GPU Skinning to greatly increase the rendering speed of skinned meshes.

**Configuration**

_Power Mode_

* Controls the GPU Clock frequency
	* Mode A (Normal)
	* Mode B (GPU High - No WLAN or COM)
	* Mode C (GPU High - No Camera, OLED Low brightness)

More information can be found at [https://psvita.scedev.net/docs/vita-en,Power-Overview-vita,Power_Configuration_Control/1/](https://psvita.scedev.net/docs/vita-en,Power-Overview-vita,Power_Configuration_Control/1/)


_Override PSVita Music_

* Acquires the PS Vita's BMG port pausing any background music which might be playing

**Optimization**

_API Compatibility Level_

* .NET 2.0
	* This is close to the full .NET 2.0 API and offers the best compatibility with pre-existing .NET code. Application's build size and startup time may be relatively poor.
* .NET 2.0 Subset
	* This is close to the Mono "monotouch" profile. The advantage of using this profile is reduced build size (and startup time) but this comes at the expense of compatibility with existing .NET code.

Note that .Net 2.0 subset has limited compatibility with other libraries. More information can be found at [http://docs.xamarin.com/guides/ios/advanced_topics/limitations/](http://docs.xamarin.com/guides/ios/advanced_topics/limitations/) 

_AOT Compilation Options_

* Allows you to set compilation options for the mono Ahead Of Time compiler.

_Stripping Level_

* Setting a Stripping Level in the Player Settings can potentially reduce your game's memory footprint quite considerably. The options are:
	* Disabled
	* Strip Assemblies
	* Stip ByteCode
	* Use micro mscorlib

These optimisation levels are cumulative, so level 3 optimisation implicitly includes levels 2 and 1, while level 2 optimization includes level 1.

See the [PSVita Stripping Levels](PSVitaStrippingLevels) page for detailed information.

_Optimize Mesh Data_

* Remove unused mesh components

_Mesh Video Mem_

* How many megabytes of video memory to use for mesh data before we use main memory. Typically this option is left at 0 but if you find you are running short of system memory it can be useful to increase this number.

You can use the "Mesh Video Mem" option to set aside an area of CDRAM (also referred to as VRAM) that Unity will use in preference to mapped main memory when allocating memory for mesh data, once this area is full mesh data is allocated in main memory. The option's primary purpose is to ease the pressure on main memory for games which have a large memory requirement and are struggling to fit.

CDRAM is also used for render targets and textures so setting aside an area for mesh data reduces the number of textures that can go in CDRAM so you need to decide on a sensible budget depending on how much memory is left once textures and render targets are accounted for. When running development builds the amount of available CDRAM is displayed in the TTY as "[vram avail KB / KB]" so you can use that as a guide to decide how much can be set aside for mesh data. Once CDRAM is full textures are allocated in main system memory but it's best to try and avoid this situation.


##Publishing Settings
**Live Area**

LiveArea is an area provided for each game which optionally enables the enjoyment of a game to be shared among users, thereby facilitating more active communication. The default LiveArea allows you to implement a very basic LiveArea, providing only a background image and gate image used to launch your game.

PNG is the only image format that is supported in the current version. Indexing (color reduced) is recommended.

_Background_

* 840x500 pixels in size
* 8bit

_Gate Image_

* 280x158 pixels in size

**Custom Live Area**

For a more involved user experience Unity allows you to customise LiveArea with your own images and content.

_Live Area folder_

* Specify a folder within the project assets folder that contains your Live Area data
* Note that use of a Custom Live Area will override settings in the Default LiveArea section.

The LiveArea Editor tool can be used to create your LiveArea data. The LiveArea Editor is a Windows tools that allows you to use a GUI to create or edit the XML describing the screen configuration of contents information zone of LiveArea. This tool is included in the PS Vita SDK.

Detailed information on LiveArea is available at [https://psvita.scedev.net/docs/livareastarting/1/](https://psvita.scedev.net/docs/livareastarting/1/) and information on Content Information Zone XML can be found at [https://psvita.scedev.net/docs/vita-en,LiveArea-Specifications-vita,Content_Information_Zone_XML_Specifications](https://psvita.scedev.net/docs/vita-en,LiveArea-Specifications-vita,Content_Information_Zone_XML_Specifications).
.

**Software Manual**

_Manual folder_

* Specify a folder within the project assets folder that contains your application manual

The software manual consists of a series of PNG images that are displayed when the user views the software manual.

Information on software manual image specifications can be found here::
[https://psvita.scedev.net/docs/vita-en,Content_Information-Specifications-vita,Software_Manual/1/](https://psvita.scedev.net/docs/vita-en,Content_Information-Specifications-vita,Software_Manual/1/).


###Param File
_Category_

* PS Vita Application
* PS Vita Application Patch

_Master Version_

* The Master Version is the submission version of a product, for each re-submission to SCE the master version would be incremented, i.e. 01.00, 01.01, etc.

_Application Version_

* The Application Version is used for patch updates, when you first submit your application this would be 01.00, for each patch update you would increment this, i.e. 0.1.00, 0.1.01, etc.

_Content ID_

* Packages are distinguished by ContentIDs. View `%SCE_ROOT_DIR%\PSP2\Tools\Publishing Tools\help\Publishing_Tools-Overview_e.pdf` for more information.

_Title_

* This title is displayed in the Activities section, as well as in all social communications.

_Short Title_

* The short title is displayed under your game icon on the Home Screen.

_Save data quota (KB)_

* Specifies the maximum amount of save game data that can be saved to the Vita.

_Parental Level (0-11)_

* Set the parental control level. Note that the lower the number, the tighter the restriction.

_Allow Twitter Dialog_

* If your application supports posting to Twitter you need to tick this option.

_Vita TV, disable Touch Panel Emulation by L3/R3 Buttons_

* Disables touch panel emulation.

_Vita TV Boot Mode_

* Default (Managed by System Software (SCEE or SCA)
* PS Vita Bootable, PS Vita TV Bootable (SCEJ or SCE Asia)
* PS Vita Bootable, PS Vita TV Not Bootable (SCEJ or SCE Asia)

_Memory Expansion Mode_

The memory size of the main memory's physical memory to be used by the application can be expanded by setting a Memory Mode. 

Available modes include:

* 29MiB - Only this app can be run
* 77MiB - Only this app can be run, the internet browser cannot be used
* 109MiB - Only this app can be run, the internet browser and title store cannot be used

The option for Memory Expansion Mode is available in the player settings in the Param File section.

This setting cannot be changed dynamically.

Detailed informaiton on Memory Expansion Mode can be found in the SDK documentation at [https://psvita.scedev.net/docs/vita-en,Programming-Startup_Guide-vita,Resources_that_Can_Be_Used_by_an_Application/1/](https://psvita.scedev.net/docs/vita-en,Programming-Startup_Guide-vita,Resources_that_Can_Be_Used_by_an_Application/1/)

_Param File (param.sfx)_

* The location of your self-made param.sfx file, if a file is specified here then the contents of the param.sfx file will override all of the above package parameter settings. This can be useful if you plan to submit your application in multiple territories which require slightly different parameters.

More information about creating parameter files can be found at `%SCE_ROOT_DIR%\PSP2\Tools\Publishing Tools\help\Param_File_Editor-Users_Guide_e.pdf` and `%SCE_ROOT_DIR%\PSP2\Tools\Publishing Tools\help\Publishing_Tools-Overview_e.pdf`

**Package**

_Password (32 chars)_

* A passcode is randomly generated by the Unity Editor, you can use your own if you prefer. The Playstation(R)Vita requests the passcode when reading installed components to prevent unauthorised reads for other installed applications.

_Cumulative Patch_
It is possible to build a patch package using the Cumulative Patch settings.

_Change Info Folder_

* Path to your 'Change Info' XML file

_First Published Package_

* Path to the initial version/package of your game. This must be the package that was first submitted and accepted by SCE.

More information on cumulative patch can be found at [https://psvita.scedev.net/docs/vita-en,Patch-Overview-vita,PlayStationregVita_Patch_System/1/](https://psvita.scedev.net/docs/vita-en,Patch-Overview-vita,PlayStationregVita_Patch_System/1/).

**Digital Rights Management**

DRM content is a product provided in the form of downloadable software. The DRM Type allows you to choose the type of DRM (Digital Rights Management) protection for your package.

* DRM Type 
	* Paid-for content (Local)
	* Free content (Free)

Information on DRM content can be found at [https://psvita.scedev.net/docs/vita-en,NP_Commerce-Overview-vita,Products/1/](https://psvita.scedev.net/docs/vita-en,NP_Commerce-Overview-vita,Products/1/).

**Media Type & Size**

_Storage Type_

* No VC/MC-MC
	* This application is not distributed by PS Vita card(VC)
	* This application is distributed by network and installed on to memory card(MC)
* VC-VC
	* This application is distributed by PS Vita card(VC)
	* This application may be distributed by network and installed on to memory card(MC)
	* In case of VC Distribution - the VC has rewritable(R/W) area, and Patches/Additional Contents/Save Data are stored on R/W area of the VC. MC is not required to run this application
	* VC-MC

Information on the types of Package Configuration / Storage Types is available at [https://psvita.scedev.net/docs/vita-en,Development_Process-Overview-vita,Application_Package_Configuration/1/](https://psvita.scedev.net/docs/vita-en,Development_Process-Overview-vita,Application_Package_Configuration/1/).

_Media Capacity_

* Selectable VC-VC Capacities
	* VC 2GB (R\O:1312Mib, R\W:480Mib)
	* VC 2GB (R\O:1504Mib, R\W:288Mib)
	* VC 2GB (R\O:1696Mib, R\W:96Mib)
	* VC 2GB (R\O:2624Mib, R\W:960Mib)
	* VC 2GB (R\O:3008Mib, R\W:576Mib)
	* VC 2GB (R\O:3392Mib, R\W:192Mib)
* Selectable VC-MC Capacities
	* VC 2GB (R\O:1792Mib, R\W:On MC)
	* VC 2GB (R\O:3584Mib, R\W:On MC)

**Playstation(R)Network**

Supports Game Boot Message and/or Game Joining Presence

* Note that you must set the NP Communications ID (see below)

_Trophy Pack_

* Specify the location of your trophy pack file (*.trp)

Note that you must set the NP Communications ID in Player Settings and that must match the NP Communications ID specified in the trophy pack.

The Trophy Pack File Utility can be used to create and modify your trophy pack. The Trophy Pack File Utility  is a Windows application that comes with the PS Vita SDK.

More information on trophy packs and creating trophy packs can be found at: [https://psvita.scedev.net/docs/vita-en,Trophy_System-Overview-vita,Designing_the_Trophy_Set/1/](https://psvita.scedev.net/docs/vita-en,Trophy_System-Overview-vita,Designing_the_Trophy_Set/1/) and [https://psvita.scedev.net/docs/vita-en,Trophy_System-Overview-vita,Trophy_Configuration_Data/1/](https://psvita.scedev.net/docs/vita-en,Trophy_System-Overview-vita,Trophy_Configuration_Data/1/) and `%SCE_ROOT_DIR%\PSP2\Tools\Publishing Tools\help\Trophy_Pack_File_Utility-Users_Guide_e.pdf`


_NP Communication ID_

* An NP Communication ID can be requested for, and issued, per application via the PlayStation(R)Vita Developer Network

_NP Communication Passphrase_

* Enter the NP Communication Passphrase provided by via the PlayStation(R)Vita Developer Network

_NP Communication Signature_

* Enter the NP Communication Signature provided by via the PlayStation(R)Vita Developer Network

The Unity Vita Add-on includes a package called `[PSVita Samples]NP Toolkit.unitypackage` that contains a native plugin and managed assembly that provides a scripting interface to the Playstation Network services along with example scripts.
