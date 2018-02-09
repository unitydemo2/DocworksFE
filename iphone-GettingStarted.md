#Getting started with iOS development

Building games for devices like the iPhone and iPad requires a different approach than you would use for desktop PC games. Unlike the PC market, your target hardware is standardized and not as fast or powerful as a computer with a dedicated video card. Because of this, you will have to approach the development of your games for these platforms a little differently. Also, the features available in Unity for iOS differ slightly from those for desktop PCs.

##Setting up your Apple Developer account

You don't need an Apple Developer account to build to devices; any Apple ID is sufficient for building only to your own device for testing. 

However, we recommend that you set up your Apple Developer account before proceeding because you will need it to use Unity to its full potential with iOS. This includes establishing your team, adding your devices, and finalizing your provisioning profiles. All this setup is performed through Apple's Developer website. Since this is a complex process, we have provided a [basic outline](iphone-accountsetup) of the tasks that must be completed, which can be referred to alongside the step-by-step instructions at [Apple's iPhone Developer portal](http://developer.apple.com/iphone).



##The Unity XCode project

When you build the Unity iOS game an XCode project is generated. This project is required to sign, compile and prepare your game for distribution. See the [Unity XCode project](StructureOfXcodeProject) manual page for further information.



##Accessing iOS functionality

Unity provides a number of scripting APIs to access the multi-touch screen, accelerometer, device geographical location system and much more. You can find out more about the script classes on the [iOS scripting page](iphone-API).



##Exposing native C, C++ or Objective-C code to scripts

Unity allows you to call custom native functions written in C, C++ or Objective-C directly from C# scripts. To find out how to bind native functions, visit the [plugins page](Plugins).



##Prepare your application for in-app purchases

The Unity iOS runtime allows you to download new content and you can use this feature to implement in-app purchases. See the [downloadable content](iphone-Downloadable-Content) manual page for further information.


##Splash screen customization

See the [splash screen customization page](MobileCustomizeSplashScreen) to find out how to change the image your game shows while launching.


##Troubleshooting and reporting crashes

If you are experiencing crashes on the iOS device, please consult the [iOS troubleshooting](TroubleShootingIPhone) page for a list of common issues and solutions. If you can't find a solution here then please file a bug report for the crash (menu: __Help &gt; Report A Bug__ in the Unity editor).



##How Unity's iOS and desktop targets differ

###Statically typed JavaScript
Dynamic typing in JavaScript is always turned off in Unity when targetting iOS (this is equivalent to `#pragma strict` getting added to all your scripts automatically). Static typing greatly improves performance, which is especially important on iOS devices. When you switch an existing Unity project to the iOS target, you will get compiler errors if you are using dynamic typing. You can easily fix these either by using explicitly declared types for the variables that are causing errors or taking advantage of type inference.

###Audio compression
Unity supports importing a variety of source format sound files. However when importing these files (with the exception of tracker files), they are always re-encoded to the build target format. By default, this format is Vorbis, though this can be overridden per platform to other formats (ADPCM, MP3 etc) if required. Mp3 playback offers a little better performance on iPhone compared with Vorbis playback.

###PVRTC instead of DXT texture compression
Unity iOS does not support DXT textures. Instead, PVRTC texture compression is natively supported by iPhone/iPad devices. Consult the [texture import settings](class-TextureImporter) documentation to learn more about iOS texture formats.

###Movie playback
MovieTextures are not supported on iOS. Instead, full-screen streaming playback is provided via scripting functions. To learn about the supported file formats and scripting API, consult the [movie page](class-MovieTexture) in the manual.


