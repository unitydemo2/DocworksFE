#Features currently not supported by Unity Tizen

##Graphics

* DXT texture compression is not supported; use PVRTC formats instead. Please see the [Texture2D Component page](class-TextureImporter) for more information.
* Rectangular textures can not be compressed to PVRTC formats.
* Movie Textures are not supported; use a full-screen streaming playback instead. Please see the [Movie playback page](class-MovieTexture) for more information.


##Audio

* Ogg audio compression is not supported. Ogg audio will be automatically converted to MP3 when you switch to Tizen platform in the Editor. Please see the [AudioClip Component page](class-AudioClip) for more information about audio support in Unity Tizen.


##Scripting

* Dynamic features like Duck Typing are not supported. Use `#pragma strict` for your scripts to force the compiler to report dynamic features as errors.
* Video streaming via __WWW__ class is not supported.
* FTP support by __WWW__ class is limited.



##External Libraries

It is recommended to minimize your references to external libraries, because 1 MB of .NET CIL code roughly translates to 3-4 MB of ARM code. For example, if your application references System.dll and System.Xml.dll then it means additional 6 MB of ARM code **if stripping is not used**. At some point application will reach limit when linker will have troubles linking the code. If you care a lot about application size you might find C# a more suitable language for your code as is has less dependencies than JavaScript.
