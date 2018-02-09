Build Settings
=====

Player build settings can be found by going File -&gt; Build Settings. When building your project you can configure the following options:

## Build Type
* **Development** - build for regular development and profiling. Has additional error checks compared to **Master**
* **Master** - build meant for mastering process and submitting to LotCheck

## Build Output
* **Unpackaged** - plain files for the build are written without any further packaging
* **WUMAD file** - master archive image created from plain files. Useful for testing by hard-disk emulation, and for submission of titles for publication
* **Download image** - creates a downloadable image which can be copied to SD card and installed onto internal memory of a devkit or a CAT-R
	
## Boot Mode
* **PCFS** - the build runs from the host PC
* **NAND** - this boot mode more closely resembles final retail systems

### Common problems related to Boot Mode, include:
			
* When devkit is configured to run in **NAND** **Boot Mode** and the application is built with **PCFS**, launching the application will result in loading and running the *default title*, which is "System Config Tool".
* **NAND** **Boot Mode** build restricts memory usage to that of a retail system. if the application is running out of memory with **NAND**, but not with **PCFS** - then the devkit is configured to use 2GB development mode.   

## Script Only Build

* When building player, only scripts are compiled skipping any asset processing. This allows to make faster builds when you tweak only scripts and there's no need to reexport the asset data. 

## Autoconnect Profiler
* Enable/disable profiler auto-connect behaviour when your application is started. When this option is enabled, the editor will open profiler window and establish a connection automatically when the player launches on Wii U.

