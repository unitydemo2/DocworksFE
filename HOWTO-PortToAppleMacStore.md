#How to deliver an application to the Apple Mac Store

![](../uploads/Main/AppleMacStore.jpg) 

* Make sure you have the correct provisioning profiles installed in Organiser. Also check provisioning profile in System Preferences -&gt; Profiles.

* Create high res iconset. Make a folder named UnityPlayer.iconset (or whatever your info.plist is setup to show) with the following image names inside. Make sure the folder has the `.iconset` extension.

````
	icon_16x16.png
	icon_16x16@2x.png
	icon_32x32.png
	icon_32x32@2x.png
	icon_128x128.png
	icon_128x128@2x.png
	icon_256x256.png
	icon_256x256@2x.png
	icon_512x512.png
	icon_512x512@2x.png
````

* Make sure that the @2x images are sized 2X the image the name says. So `512x512@2x` is actually a 1024x1024 image with 144 dpi. From the Terminal, navigate to the directory where the .iconset directory is located and perform the command

````
	iconutil -c icns UnityPlayer.iconset
````

* Create an `info.plist` and an `GAMENAME.entitlements` file. The easiest way to do this is by using [http://macdownload.informer.com/unity-entitlements-tool/download/](http://macdownload.informer.com/unity-entitlements-tool/download/) to generate them for you. You can also extract the info.plist from the Unity generated .app and modify that one. The most basic `GAMENAME.entitlements` looks like this, it will make sure your app runs in the Apple sandbox. This one has no iCloud support: 

````
 <?xml version="1.0" encoding="UTF-8"?>
 <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
 <plist version="1.0">
 <dict>
 <key>com.apple.security.app-sandbox</key> <true/>
 </dict>
 </plist>
````

* Modify the following sections of the `info.plist` file to make it suitable for your app:

````
<key>CFBundleDevelopmentRegion</key>
<string>{YOUR REGION}</string>
<key>CFBundleGetInfoString</key>
<string>{DESCRIPTIVE INFO}</string>
<key>CFBundleIdentifier</key>
<string>com.{YOUR COMANY}.{YOUR APP NAME}</string>
<key>CFBundleName</key>
<string>{YOUR APP NAME}</string>
<key>CFBundleShortVersionString</key>
<string>{VERSION NUMBER, e.g. 1.0.0}</string>
<key>CFBundleSignature</key>
<string>{4 LETTER CREATOR CODE, e. g.:  GMAD }</string>
<key>CFBundleVersion</key>
<string>{VERSION NUMBER, e.g. 100}</string>
````

* Add this key to the `info.plist` file :

````
<key>LSApplicationCategoryType</key>
<string>{VALID APP CATEGORY, e.g.: public.app-category.kids-games }</string>
````

* Fix Macbook Pro Retina fullscreen problems (see [http://forum.unity3d.com/threads/145534-Mountain-Lion-MacBook-Pro-Retina-gt-problem-for-Unity-games](http://forum.unity3d.com/threads/145534-Mountain-Lion-MacBook-Pro-Retina-gt-problem-for-Unity-games)) by adding something like this. It only needs to be called once! It will create a flicker since it goes out and in fullscreen.

````
  if (Screen.fullScreen)
  {
      //MacBook Pro Retina 15: width = 2880 , MacBook Pro Retina 13: width = 2496 ?
      //could check device model name, but not sure now about retina 13 device model name
      //if last resolution is almost retina resolution...
      var resolutions : Resolution[] = Screen.resolutions;
      if (resolutions.length && resolutions[resolutions.length - 1].width > 2048)
      {
          Screen.fullScreen = false;
          yield;
          Screen.fullScreen = true;
          yield;
      }
  }
````

* Enable UseMacAppStoreValidation toggle in the PlayerSettings
* Run Unity and build the .app
* Replace the iconset.icns with the created on in Step 2 by right clicking the .app and Show Contents
* (Optional) Replace the UnityPlayerIcon in the .app with your own
* Replace the info.plist in the .app with the modified one from Step 2.
* Fix read permissions on all the content in the .app. In the Terminal type: 

````
 chmod -R a+xr "/path/to/GAMENAME.app"
````

* Sign the .App with the created entitlements from Step 3. In the Terminal type: 

````
 codesign -f --deep -s '3rd Party Mac Developer Application: DEVELOPER NAME' --entitlements "GAMENAME.entitlements" "/AppPath/GAMENAME.app"
````

* Build the installer/pkg. In the Terminal type: 

````
 productbuild --component GAMENAME.app /Applications --sign "3rd Party Mac Developer Installer: DEVELOPER NAME" GAMENAME.pkg
````
* Submit using the ApplicationLoader! Make sure your _application_id_ in iTunesConnect is in the _waiting for upload_ state.
