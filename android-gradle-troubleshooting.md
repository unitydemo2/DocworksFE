<!-- Anchor tags on this page are linked to from within the Unity Editor -->

# Gradle troubleshooting

If you just switched to export your Android project using Gradle instead of the old system, you may encounter build errors, especially if you are using additional Android libraries, or if you have added a custom __AndroidManifest.xml__.

The Android Gradle plug-in is much more picky than the old ADT/Ant system. It does not accept
anything it considers an error, whether it's duplicate symbols, references to resources that don't
exist, or a library project that sets the same attribute as the main application.

In most cases, fixing the problem involves editing an __AndroidManifest.xml__ file; either the main
one, or one from a library your project uses.

In a non-trivial project, or if the project has issues not described by the troubleshooting section
below, export the project as a Gradle project (from __Build Settings__) and build from the command line. Building from the command line gives you more detailed error messages, and makes for a quicker turnaround when applying changes.

## Specific problems

### Resource not found [resource-not-found]

An __AndroidManifest.xml__ file, either the main one or in a library, references a non-existing
resource. Often it is the application icon or label string that is set by a library. This can
happen if you have copied your main manifest to a library project without removing those references.

Remove the attribute from one of the Android Manifests -- normally the one from the library.

### Duplicate files in APK [duplicate-files-in-apk]

You have a file name collision between your main application and a library project, or between two
library projects. Keep in mind that all of the files are copied into the same APK package.

You need to remove one of the files.

### Colliding package names [colliding-package-names]

A library can not use the same Java package as the main application, or any other library.

Usually, you should change the package name of the library to something different. If the library
contains a lot of code, it may be easier to change the main package name (from _Player Settings_).

### Colliding attributes [colliding-attributes]

A library can not freely override attributes from the main __AndroidManifest.xml__.  Often this error is caused by a library setting the application icon or label string, similar to the __Resource not found__ problem above.

Either remove the attribute from the library, or add a __tools:replace__ attribute to your
__application__ tag, to indicate how the merge conflict should be resolved.

<!-- Add empty lines so that web page can be positioned with linked header on top -->
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
