# Remote Settings

Use the [Unity Analytics Service](UnityAnalytics) __Remote Settings__ feature to change variables in your game or application directly from the Analytics Dashboard. For example, if you are concerned that some levels in your game might be too hard or too easy, you can create settings that control the difficulty of your level bosses. Then, if your Analytics data shows that certain level bosses are too tough or too weak, you can tune the gameplay without releasing an update. You can even use segments to apply different settings to different groups of players. 

Remote Settings can help you:

* Adapt your game to different types of players
* Tune the game difficulty curve in near real time
* Roll out new features gradually while monitoring impact
* Tailor game settings to different regions or other player segments
* Turn seasonal, holiday, or other time-sensitive features on and off
* Test your ideas and designs

After you make changes to your Remote Settings, every computer or device starting a new session of your application downloads the new configuration values. No update to the application is necessary. You can connect Remote Settings to individual GameObject properties, or you can read the key-value pairs directly in code and [provide your own logic](UnityAnalyticsRemoteSettingsScripting) for handling setting changes.

This section describes [creating and changing Remote Settings](UnityAnalyticsRemoteSettingsCreating), and [using Remote Settings in a Unity Project](UnityAnalyticsRemoteSettingsUsing).

---

* <span class="page-edit">2017-08-28 <!-- include IncludeTextAmendPageNoEdit --></span>

* <span class="page-edit">2017-08-28 - Service compatible with Unity 5.5 onwards at this date but version compatibility may be subject to change.</span>
 
* <span class="page-history">New feature in [2017.1](https://docs.unity3d.com/2017.1/Documentation/Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>

* <span class="page-history">Added segmented Remote Settings: set different values for different segments in 2017.1</span>