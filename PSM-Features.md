Features specific to Unity for PSM
====

This document provides an explanation regarding unique specifications of Unity for PSM.

## Macro Definition

``UNITY_PSM`` macro is defined automatically when switching to PlayStation&#174;Mobile platform.

````
void OnGUI()
{
#if UNITY_PSM
    GUILayout.Box("UNITY_PSM is defined.");
#else
    GUILayout.Box("UNITY_PSM is not defined.");
#endif
}
````

## Key Assignments for PS Vita

The hardware buttons of the PS Vita are mapped both to ``KeyCode`` enum, and in the [Input Manager](class-InputManager).

See [PS Vita Input](PSM Input) for details.

## The PS Vita Touch Panel

The touchscreen is implemented through the standard Input class. Documentation specific to ``Input.touches`` is available [here](ScriptRef:Input-touches.html). As a quick example, to iterate through each current touch you would use the code:

````
	void OnGUI () {
		GUILayout.Box(string.Format("mousePosition={0}, {1}, {2}", Input.mousePosition.x, Input.mousePosition.y, Input.mousePosition.z));

		for (int i = 0; i < Input.touchCount; ++i)
		{
			Vector2 pos = Input.GetTouch(i).position;
			GUI.Label(new Rect(pos.x, Screen.height - pos.y, 50, 30), "(X) #" + i);
		}
	}
````

The rear touch pad is implemented through the ``UnityEngine.PSM.PSMInput`` class. For example, to iterate through each of current touch you would use the code:

````
	using UnityEngine.PSM;
	void OnGUI () {
		foreach (Touch touch in PSMInput.touchesSecondary)
		{
			Vector2 pos = touch.position;
			GUI.Label(new Rect(pos.x, Screen.height - pos.y, 50, 30), "(X) #" + touch.fingerId);
		}
	}
````

## PS Vita Logs

Strings output by PS Vita are displayed to Publishing Utility for Unity's [Package & App] panel - [Console Output].

Note: Logs will not be displayed when starting DevAssistant after starting Publishing Utility for Unity. Start DevAssistant and then start Publishing Utility for Unity.

The log output can also be retrieved using the [PsmDeviceForUnity.exe](PSMPsmDevice) command line tool.

## Project Structure

### Special directories

* ``/path/to/project/Assets/StreamingAssets`` : for assets that Unity should not process.
  Will be available as ``/Application/Data/StreamingAssets/*`` (or [Application.streamingAssetsPath](ScriptRef:Application-streamingAssetsPath)) when running on the device.\
  Useful for binary such as
    * Videos
    * Asset bundles
    * Custom assets
* ``/path/to/project/Assets/Plugins/PSM/`` : for the PSM manifest (app.xml) and any PSM specific plugins.

## Runtime paths
PSM allows read/read&write access to 3 folders when running on the device:

**``/Application``**

* Read-only folder where the application content is stored.
* This the base path for [Application.dataPath](ScriptRef:Application-dataPath) and [Application.streamingAssetsPath](ScriptRef:Application-streamingAssetsPath).

**``/Documents``**

* Read/write folder where the application can store persistent data. This folder is guaranteed to be kept between application launches/upgrades.
* This is equivalent to [Application.persistentDataPath](ScriptRef:Application-persistentDataPath).

**``/Temp``**

* Read/write folder where the application can store transient data. This folder may be cleared when the application is no longer running.
* This is equivalent to [Application.temporaryCachePath](ScriptRef:Application-temporaryCachePath).

## PlayerPrefs

Unity for PSM also supports the [PlayerPrefs](ScriptRef:PlayerPrefs) API to store and retrieve player data. For PSM this file is stored as ``/Documents/playerprefs.bin``.
This means that the contents are also available as a regular file using ``System.IO.File`` etc, and that it can be transferred/backed up etc.

One thing to remember is that in order to actually update the on-disk representation the application must call [PlayerPrefs.Save()](ScriptRef:PlayerPrefs.Save).


## About Uninstallation

To uninstall PSM Tool Set, execute one of the following.

* Select [Start] - [All Programs] - [PSM Tool Set for Unity] - [Uninstall] .
* From [Control Panel] - [Program and Features] , select and uninstall [SCE PlayStation&#174;Mobile Tool Set for Unity] .

Also note that please quit the PSM DevAssistant for Unity and disconnect a USB cable before proceeding with the uninstall.

Note: There is no specific order in which Unity Editor and PSM Tool Set must be uninstalled.

