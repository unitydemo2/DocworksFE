Windows Phone 8: Plugins
========================


Windows Phone 8 plugins work almost identically to Windows Store plugins. They enable access to types in [.NET for Windows Phone](http://goo.gl/rvbZv) that would otherwise be inaccessible from Unity. Two assemblies must be compiled with identical names and interfaces. By interface we mean public type names, methods, properties, etc. One of them is placed in Assets\Plugins folder and is used by the Editor. Another one (with Windows Phone 8 specific implementation) should be placed in Assets\Plugins\WP8 folder. During the build process it will overwrite default plugin and will be used on the actual device.

