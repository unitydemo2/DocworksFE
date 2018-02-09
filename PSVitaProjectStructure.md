PS Vita Project Structure
===

##Special directories

* `/path/to/project/Assets/StreamingAssets` : for assets that Unity should not process. Will be packaged as `Media/StreamingAssets/*`.
	* Videos
	* Asset bundles
	* Custom assets
* `/path/to/project/Assets/Plugins/PSVita/` : for native plugins. `*.sprx` and `*_stub.a`. Will be packaged as `Media/Plugins/*`.

##Runtime paths:
The Vita Dev Kit will mount the game folder depending on the Build Type:

**PC Hosted**

* Game folder mounted on the development machine at `host0:/`. This location can be viewed in the Neighborhood for Playstation(R)Vita.

**Package**

* Game folder mounted on the device at `app0:/gameName`.


More information on Mount Points can be found at  [https://psvita.scedev.net/docs/vita-en,Development_Process-Overview-vita,Mount_Points/1/](https://psvita.scedev.net/docs/vita-en,Development_Process-Overview-vita,Mount_Points/1/).
