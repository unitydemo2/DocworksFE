# Remote Settings network requests

When you [create a Remote Settings key-value pair](UnityAnalyticsRemoteSettingsCreating) in the Unity Analytics Dashboard, the Unity Analytics Service stores that setting in the __Configuration__ for your project that you have specified (either the __Release__ or the __Development__ configuration). Whenever a player starts a new session of your application, Unity makes a network request for the latest configuration from the Analytics Service. Unity considers a new session to have started when the player launches the application, or returns to an application that has been in the background for at least 30 minutes. Unity requests the __Release__ configuration when running regular, non-development builds of your application, and requests the __Development__ configuration when running development builds. Play mode in the Unity Editor counts as a development build.

**Note:** For Unity to request the __Development__ configuration, you must build the application with Unity version 5.6.0p4+, 5.6.1p1+, 2017.1+, or Unity 5.5.3p4+, and tick the __Development Build__ checkbox on the [Build Settings window](BuildSettings). If you build the game with an older version of Unity, Unity always requests the __Release__ configuration.

When the network request for the Remote Settings configuration is complete, the [RemoteSettings](ScriptRef:RemoteSettings.html) object dispatches an `Updated` event to any registered event handlers, including those registered by [Remote Settings components](UnityAnalyticsRemoteSettingsComponent).  

If the computer or device has no Internet connection and cannot communicate with the Analytics Service, Unity uses the last configuration it received and saved. The `RemoteSettings` object still dispatches an `Updated` event when using a saved configuration. However, if Unity has not saved the settings yet (such as when a player has no network connection the first time they run your game), then the `RemoteSettings` object does not dispatch an `Updated` event, and so does not update your game variables. Requesting the Remote Settings configuration over the network is an asynchronous process that might not complete before your initial Scene has finished loading, or might not complete at all, so you should always initialize your game variables to reasonable defaults.

**Note:** The web service from which Unity downloads the Remote Settings configuration is read-only, but is not secured. This means that the configuration could be read by third-parties. You should not put sensitive or secret information into your Remote Settings. Similarly, the saved settings file could be read and modified by end-users (although any modifications are overwritten the next time a session starts with an available Internet connection).

---

* <span class="page-edit">2017-05-30 <!-- include IncludeTextNewPageYesEdit --></span>

* <span class="page-edit">2017-05-30 - Service compatible with Unity 5.5 onwards at this date but version compatibility may be subject to change.</span>
 
* <span class="page-history">New feature in 2017.1</span> 
