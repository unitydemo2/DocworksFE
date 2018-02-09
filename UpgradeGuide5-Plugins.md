#Plugins in Unity 5.0

These are notes to be aware of when upgrading projects from Unity 4 to Unity 5, if your project uses plugins, including native audio plugins.

Plugins are no longer required to be placed in Assets\Plugins\<Platform> folders, they now have settings for checking which platforms are compatible and platform specific settings (like setting compatible CPU, SDK's) etc. By default new plugins are marked as compatible with 'Any Platform'. To make transition easier from older Unity versions, Unity will check in what folder plugin is located, and set initial settings accordingly, for ex., if plugin is located in Assets\Plugins\Editor, it will be marked as compatible with Editor only, if plugin is located in Assets\Plugins\iOS, it will be marked as compatible with iOS only, etc. Also please refer to 'PluginInspector documentation' for more info.

###Native Plugins in the Editor

32-bit native plugins will not work in the 64-bit editor.  Attempting to load them will result in errors being logged to the console and exceptions being thrown when trying to call a function from the native plugin.

To continue to use 32-bit native plugins in the editor, use the 32-bit editor version (provided as a separate installer).

To have both 32-bit and 64-bit versions of the same plugin in your project, simply put them in two different folders and set the supported platforms appropriately in the importer settings.

Restrictions:

 - We currently do not provide a 32-bit editor for OSX.

###Native Audio Plugins

Plugins with the prefix "audioplugin" (case-insensitive) will be automatically loaded upon scanning so that they are usable in the audio mixer. The same applies to standalone builds where these plugins are loaded at startup time before any assets have yet been loaded, as certain assets such as audio mixers require them to be loaded in order to instantiate effects.
