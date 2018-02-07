#AAR plug-ins and Android Libraries

##AAR plug-ins

Android Archive (AAR) plug-ins are bundles that include compiled Java and native (C/C++) code, resources, and an Android Manifest. The .aar file itself is a zip archive which contains all of the Assets. For more details, see [Android Developer documentation on creating an Android Library](https://developer.android.com/studio/projects/android-library.html#aar-contents). 

To add an AAR plug-in to your project, copy the .aar file into any of your project folders, then select it in Unity to open the Import Settings in the Inspector window. Tick the __Android__ checkbox to mark this .aar file as compatible with Unity:


![ARR plug-in import settings as displayed in the Inspector window](../uploads/Main/AndroidARRPlugins.png)

AAR is the recommended plug-in format for Unity Android applications.


##Android Library Projects
Android Library projects are similar to AAR plug-ins: they contain native and Java code, resources, and an Android Manifest. However, an Android Library is not a single archive file, but a directory with a special structure which contains all of the Assets. For more details, see [Android Developer documentation on creating an Android Library](https://developer.android.com/studio/projects/android-library.html#aar-contents).


Import pre-compiled Android library projects into the Assets/Plugins/Android folder. Pre-compiled means that all .java files must have been compiled into .jar files and placed in either the bin/ or the libs/ folder of the Android Studio project before being imported into Unity. From these folders, AndroidManifest.xml gets automatically merged with the main manifest file when the project is built.

Unity treats any subfolder of Assets/Plugins/Android as a potential Android Library, and disables Asset importing from within these subfolders. The subfolder is recognized as an Android Library if it contains the AndroidManifest.xml file, and the project.properties file contains the string `android.library=true`.

[See Android Developer documentation on the Library module](https://developer.android.com/studio/projects/index.html#ApplicationModules) for more details.

##Providing additional Android Assets and resources

If you need to add Assets to your Unity application that should be copied unchanged into the output package, import them into the Assets/Plugins/Android/assets directory. They appear in the assets/ directory of your APK, and are accessed by using the [getAssets()](https://developer.android.com/reference/android/content/res/Resources.html#getAssets()) Android API from your Java code.

<br/>

----
* <span class="page-edit">2017-05-18  <!-- include IncludeTextNewPageYesEdit --></span>

* <span class="page-history">Updated features in 5.5</span>
