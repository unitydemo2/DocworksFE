#Special folders and script compilation order

Unity reserves some project folder names to indicate that the contents have a special purpose. Some of these folders have an effect on the order of script compilation. These folder names are: 

* Assets
* Editor
* Editor default resources
* Gizmos
* Plugins
* Resources
* Standard Assets
* StreamingAssets

See [Special folder names](SpecialFolders) for information on what these folders are used for.

There are four separate phases of script compilation. The phase where a script is compiled is determined by its parent folder.

This is significant in cases where a script must refer to classes defined in other scripts. The basic rule is that anything that is compiled in a phase *after* the current one cannot be referenced. Anything that is compiled in the current phase or an earlier phase is fully available.

Another situation for this occurs when a script written in one language must refer to a class defined in another language (for example, a UnityScript file that declares variables of a class defined in a C# script). The rule here is that the class being referenced must have been compiled in an earlier phase.

The phases of compilation are as follows:

* **Phase 1:** Runtime scripts in folders called __Standard Assets__, __Pro Standard Assets__ and __Plugins__.
* **Phase 2:** Editor scripts in folders called __Editor__ that are anywhere inside top-level folders called __Standard Assets__, __Pro Standard Assets__ and __Plugins__.
* **Phase 3:** All other scripts that are not inside a folder called __Editor__.
* **Phase 4:** All remaining scripts (those that are inside a folder called __Editor__).


A common example of the significance of this order occurs when a UnityScript file needs to reference a class defined in a C# file. To achieve this, you need to place the C# file inside a Plugins folder, and the UnityScript file in a non-special folder. If you don't do this, an error is thrown saying that the C# class cannot be found.

**Note:** Standard Assets work only in the __Assets__ root folder.
