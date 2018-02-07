#Other Upgrade Notes for Unity 5.0

More information about features that have changed and may affect your project when upgrading from Unity 4 to Unity 5

## Locking / Hiding the Cursor

Cursor lock and cursor visibility are now independent of each other.

````
// Unity 4.x
Screen.lockCursor = true;
````
 
````
// Becomes this in Unity 5.0
Cursor.visible = false;
Cursor.lockState = CursorLockMode.Locked;
````

---

## Linux

Gamepad handling has been reworked for Unity 5.

Unity is now capable of "configuring" gamepads - either via a database of known models, or using the SDL_GAMECONTROLLERCONFIG environment variable, which is set by Steam Big Picture / SteamOS for gamepads detected or configured with its interface.

Configured gamepads present a consistent layout: left stick uses axes 0/1, right stick uses axes 3/4, buttons on the face of the gamepad are 0-3, etc. To determine whether a gamepad has been configured, call Input.IsJoystickPreconfigured().

---

## Windows Store Apps

'Metro' keyword was replaced to 'WSA' in most APIs, for example: BuildTarget.MetroPlayer became BuildTarget.WSAPlayer, PlayerSettings.Metro became PlayerSettings.WSA.

Defines in scripts like UNITY_METRO, UNITY_METRO_8_0, UNITY_METRO_8_1 are still there, but along with them there will be newer defines UNITY_WSA, UNITY_WSA_8_0, UNITY_WSA_8_1.

---

##Other script API changes that cannot be upgraded automatically

- UnityEngine.AnimationEvent is now a struct.  Comparisons to 'null' will result in compile errors.

- AddComponent(string), when called with a variable cannot be automatically updated to the generic version AddComponent&lt;T&gt;(). In such cases the API Updater will replace the call with a call to APIUpdaterRuntimeServices.AddComponent(). This method is meant to allow you to test your game in editor mode (they do a best effort to try to resolve the type at runtime) but it is not meant to be used in production, so it is an error to build a game with calls to such method). On platforms that support Type.GetType(string) you can try to use GetComponent(Type.GetType(typeName)) as a workaround.
 

- AssetBundle.Load, AssetBundle.LoadAsync and AssetBundle.LoadAll have been deprecated. Use AssetBundle.LoadAsset, AssetBundle.LoadAssetAsync and AssetBundle.LoadAllAssets instead. Script updater cannot update them as the loading behaviors have changed a little. In 5.0 all the loading APIs will not load components any more, please use the new loading APIs to load the game object first, then look up the component on the object.

---

##Unity Package changes

The internal package format of .unityPackages has changed, along with some behaviour of how packages are imported into unity and how conflicts are resolved.

- Packages are now only constructed with the source asset and the .meta text file that contains all the importer settings for the asset.

- Packages will always require asset importing now.

- Packages will be reduced in size significantly, because the imported data (for example texture and audio data) will not be doubled up.

- Packages with file names that already exist in the project, but with different GUIDs will have these files imported with a unique file name. This is done to prevent overriding files in the project that actually came from different packages or were created by the user.