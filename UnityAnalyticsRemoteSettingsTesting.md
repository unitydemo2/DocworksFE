# Testing Remote Settings

While you can view the keys and values of both configurations in the Editor, Unity only loads one configuration at runtime. Unity uses the Development configuration in Play mode and in any builds created with the __Development Build__ box checked on the [Build Settings window](BuildSettings). Unity uses the __Release__ configuration in non-development builds. 

Before testing Remote Settings, you must first [create the settings](UnityAnalyticsRemoteSettingsCreating) and then either use the [Remote Settings component](UnityAnalyticsRemoteSettingsComponent) or [write the code](UnityAnalyticsRemoteSettingsScripting) necessary to map the settings to variables in your game or application.

To test with the __Development__ configuration, click the __Play__ button in the Editor or:

1. Go to __File__ > __Build Settings__ to open the Build Settings window.

2. Check the __Development Build__ box.

3. Click the __Build And Run__ button.

To test with the __Release__ configuration:

4. Go to __File__ > __Build Settings__ to open the Build Settings window.

5. Uncheck the __Development Build__ box.

6. Click the __Build And Run__ button.

---

* <span class="page-edit">2017-05-30 <!-- include IncludeTextNewPageYesEdit --></span>

* <span class="page-edit">2017-05-30 - Service compatible with Unity 5.5 onwards at this date but version compatibility may be subject to change.</span>
 
* <span class="page-history">New feature in 2017.1</span> 
