#Extending the UnityPlayerActivity Java Code

When developing a Unity Android application, it is possible to extend the standard UnityPlayerActivity class (the primary Java class for the Unity Player on Android, similar to AppController.mm on Unity iOS) by using plug-ins. An application can override any and all of the basic interaction between the Android OS and the Unity Android application.


Two steps are required to override the default activity:

* Create the new [Activity](http://developer.android.com/reference/android/app/Activity.html) which derives from UnityPlayerActivity;

* Modify the [Android Manifest](android-manifest) to have the new activity as the application’s entry point.


The easiest way to achieve this is to export your project, and make the necessary modifications to the UnityPlayerActivity class in Android Studio.

To make a plug-in with your new activity code and add it to your Unity project you must perform the following steps:

1. Extend the UnityPlayerActivity. The UnityPlayerActivity.java file is found at _/Applications/Unity/Unity.app/Contents/PlaybackEngines/AndroidPlayer/src/com/unity3d/player_ on Mac and _C:\Program Files\Unity\Editor\Data\PlaybackEngines\AndroidPlayer\src\com\unity3d\player_ on Windows. To extend the UnityPlayerActivity locate the classes.jar included with Unity. It is found in the installation folder (usually C:\Program Files\Unity\Editor\Data (on Windows) or /Applications/Unity (on Mac)) in a subfolder called PlaybackEngines/AndroidPlayer/Variations/mono or il2cpp/Development or Release/Classes/. Then add classes.jar to the classpath used to compile the new Activity. Compile your Activity source file and package it into a JAR or AAR package, and copy it to your project folder..


2. Create a new Android Manifest to set the new activity as the entry point of your application. Place the AndroidManifest.xml file in the Assets/Plugins/Android folder of your project.


The following is an example UnityPlayerActivity file: 

```
OverrideExample.java:
package com.company.product;
import com.unity3d.player.UnityPlayerActivity;
import android.os.Bundle;
import android.util.Log;

public class OverrideExample extends UnityPlayerActivity {
  protected void onCreate(Bundle savedInstanceState) {
    // call UnityPlayerActivity.onCreate()
    super.onCreate(savedInstanceState);
    // print debug message to logcat
    Log.d("OverrideActivity", "onCreate called!");
  }
  public void onBackPressed()
  {
    // instead of calling UnityPlayerActivity.onBackPressed() we just ignore the back button event
    // super.onBackPressed();
  }
}
```

```
And this is what the corresponding AndroidManifest.xml could look like:
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="com.company.product">
  <application android:icon="@drawable/app_icon" android:label="@string/app_name">
    <activity android:name=".OverrideExample"
             android:label="@string/app_name"
             android:configChanges="fontScale|keyboard|keyboardHidden|locale|mnc|mcc|navigation|orientation|screenLayout|screenSize|smallestScreenSize|uiMode|touchscreen">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>
  </application>
</manifest>
```

<br/>

----

* <span class="page-edit">2017-05-18  <!-- include IncludeTextNewPageNoEdit --></span>

* <span class="page-history">Updated features in 5.5</span>
