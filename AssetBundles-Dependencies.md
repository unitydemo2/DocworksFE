# Section 5: AssetBundle Dependencies

AssetBundles can become dependant on other AssetBundles if one or more of the `UnityEngine.Objects` contains a reference to a `UnityEngine.Object` located in another bundle.  A dependency does not occur if the UnityEngine.Object contains a reference to a `UnityEngine.Object` that is not contained in any AssetBundle.  In this case, a copy of the object that the bundle would be dependant on is copied into the bundle when you build the AssetBundles.  If multiple objects in multiple bundles contain a reference to the same object that isn’t assigned to a bundle, every bundle that would have a dependency on that object will make its own copy of the object and package it into the built AssetBundle.

Should an AssetBundle contain a dependency, it is important that the bundles that contain those dependencies are loaded before the object you’re attempting to instantiate is loaded.  Unity will not attempt to automatically load dependencies.

Consider the following example, a Material in __Bundle 1__ references a Texture in __Bundle 2__:

In this example, before loading the Material from __Bundle 1__, you would need to load __Bundle 2__ into memory.  It does not matter which order you load __Bundle 1__ and __Bundle 2__, the important takeaway is that __Bundle 2__ is loaded before loading the Material from __Bundle 1__.  In the next section, we’ll discuss how you can use the `AssetBundleManifest` objects we touched on in the previous section to determine, and load, dependencies at runtime.

----

* <span class="page-edit">2017-05-15  <!-- include IncludeTextNewPageNoEdit --></span>

