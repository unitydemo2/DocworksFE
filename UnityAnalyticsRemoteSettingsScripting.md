# Remote Settings scripting

Use the Unity Scripting API [RemoteSettings](ScriptRef:RemoteSettings.html) class to handle your settings in code. You can register a handler function for the `RemoteSettings.Updated` event. The `RemoteSettings` class calls all registered handlers whenever a new sessions starts. [Create the key-value pairs](UnityAnalyticsRemoteSettingsCreating) for the `RemoteSettings` object to download on the Unity Analytics Dashboard.

Fetching the settings requires a [network transaction](UnityAnalyticsRemoteSettingsNetRequests), so the `RemoteSettings` object dispatches the `Updated` event asynchronously. Your handler function might not be called in the same order on every platform or even on every launch of the same platform. In fact, if no network connection is available and no cached settings are found, the `RemoteSettings` object does not dispatch an `Updated` event at all. Always initialize your configuration variables with reasonable default values, and allow for the possibility that your `Updated` handler can be called at different times or in a different order. 

**Code example**

The following example shows a class that defines a number of properties for tuning game difficulty:

```
using UnityEngine;

public class RemoteTuningVariables : MonoBehaviour {
	
    public float DefaultSpawnRateFactor = 1.0f;
    public float DefaultEnemySpeedFactor = 1.0f;
    public float DefaultEnemyStrengthFactor = 1.0f;
    public static float SpawnRateFactor{ get; private set; }
    public static float EnemySpeedFactor{ get; private set; }
    public static float EnemyStrengthFactor{ get; private set; }

    void Start () {
        SpawnRateFactor = DefaultSpawnRateFactor;
        EnemySpeedFactor = DefaultEnemySpeedFactor;
        EnemyStrengthFactor = DefaultEnemyStrengthFactor;

        RemoteSettings.Updated += 
            new RemoteSettings.UpdatedEventHandler(HandleRemoteUpdate);
    }

    private void HandleRemoteUpdate(){
        SpawnRateFactor 
            = RemoteSettings.GetFloat ("SpawnRateFactor", DefaultSpawnRateFactor);
        EnemySpeedFactor
            = RemoteSettings.GetFloat ("EnemySpeedFactor", DefaultEnemySpeedFactor);
        EnemyStrengthFactor 
            = RemoteSettings.GetFloat ("EnemyStrengthFactor", DefaultEnemyStrengthFactor);
    }
} 
```

Notice that the class provides default values in the `RemoteSettings.GetFloat()` method calls. If the `RemoteSettings` object cannot find the specified key (if you misspell a key name, for example), then the method still assigns your default values to the tuning variables. Otherwise, the `GetFloat()` and `GetInt()` methods assign zero to numbers, `GetString()` assigns an empty string to strings, and `GetBool()` assigns false to boolean variables.

The class also assigns the same default values to the properties in the `Start()` method. When Unity cannot access the Analytics Service and no previously cached configuration is available locally, the `RemoteSettings` object does not dispatch the `Updated` event. Assigning the defaults in the `Start()` method ensures that the properties always have reasonable values. 

---

* <span class="page-edit">2017-05-30 <!-- include IncludeTextNewPageYesEdit --></span>

* <span class="page-edit">2017-05-30 - Service compatible with Unity 5.5 onwards at this date but version compatibility may be subject to change.</span>
 
* <span class="page-history">New feature in 2017.1</span> 
