# Using the Automatic API Updater

## Why would my code need updating?

Sometimes, during development of the Unity software, we make the decision to change and improve the way the classes, functions and properties (the API) work. We do this with a focus on causing the least impact on user's existing game code, but sometimes in order to make things better, we have to break things.

We tend to only introduce these significant "breaking changes" when moving from one significant version of Unity to another, and only in cases that it makes Unity easier to use (meaning users will incur fewer errors) or brings measurable performance gains, and only after careful alternative consideration. However, the upshot of this is that if you were to - for example - open a Unity 4 project in Unity 5, you might find some of the scripting commands that you used have now been changed, removed, or work a little differently.

One obvious example of this is that in Unity 5, we removed the "quick accessors" which allowed you to reference common component types on a GameObject directly, such as `gameObject.light`, `gameObject.camera`, `gameObject.audioSource`, etc.

In Unity 5, you now have to use the GetComponent command for all types, except transform. Therefore if you open a Unity 4 project that uses `gameObject.light` in Unity 5, you will find that particular line of code is *obsolete* and needs to be updated.

## The automatic updater

Unity has an **Automatic Obsolete API Updater** which will detect uses of obsolete code in your scripts, and can offer to automatically update them. If you accept, it will rewrite your code using the updated version of the API. 

![The API Update dialog](../uploads/Main/APIUpdaterWarningDialog.png)

Obviously, as always, it's important to have a backup of your work in case anything goes wrong, but particularly when you're allowing software to rewrite your code! Once you've ensured you have a backup, and clicked the "Go Ahead" button, Unity will rewrite any instances of obsolete code with the recommended updated version.

So, if for example you had a script which did this:

````
light.color = Color.red;
````

Unity's API updater would convert that for you to:

````
GetComponent<Light>().color = Color.red;
````

The overall workflow of the updater is as follows:

1. Open a project / import a package that contains scripts / assemblies with obsoleted API usage
2. Unity triggers a script compilation
3. API updater checks for particular compiler errors that it knows are "updatable"
4. If we find any occurrence in previous step, show a dialog to user offering automatic update, otherwise, we've finished.
5. If user accepts the update, then run API updater (which will update all scripts written in the same language being compiled in step 2)
6. Go to step 2 (to take any updated code into account) until no scripts get updated in step 5

So, from the list above you can see the updater may run multiple times if there are scripts which fall into different compilation passes (Eg, scripts in different languages, editor scripts, etc) that use obsolete code.

When the API Updater finishes successfully, you will get a notification in the console, like this:

![Success!](../uploads/Main/APIUpdaterFinishedConsoleLog.png)

If you choose *not* to allow the API updater to update your scripts, you will see the script errors in your console as normal. You will also notice that the errors which the API Updater could update automatically are marked as **(UnityUpgradable)** in the error message.

![Errors in the console, when the API updater is canceled](../uploads/Main/APIUpdaterRejectedConsoleErrors.png)

If your script has other errors, in addition to obsolete API uses, the API updater may not be able to fully finish its work until you have fixed the other errors. In this case, you'll be notified in the console window with a message like this:

![Other errors in your scripts can prevent the API updater from working properly.](../uploads/Main/APIUpdaterOtherErrors.png)

"Some scripts have compilation errors which may prevent obsolete API usages to get updated. Obsolete API updating will continue automatically after these errors get fixed."

Once you have fixed the other errors in your script, you can run the API updater again. The API updater runs automatically when a script compilation is triggered, but you can also run it manually from the Assets menu, here:

![The API Updater can be run manually from the Assets menu.](../uploads/Main/APIUpdaterMenuOption.png)

## Troubleshooting

If you get a message saying "API Updating failed. Check previous console messages." this means the API updater encountered a problem that prevented it from finishing its work.

A common cause of this is if the updater was unable to save its changes - if for example - the user does not have rights to modify the updated script. It might be write protected, for instance.

By checking the previous lines in the console as instructed, you should be able to see the problems that occurred during the update process.

![In this example the API updater failed because it did not have write permission for the script file.](../uploads/Main/APIUpdaterFailed.png)

## Limitations

Not every API change can be automatically fixed by the updater. Below is a list of the current API changes which **cannot** be fixed by the updater:

- `Mesh.GetTriangleStrip()` / `SetTriangleStrip()`
- TextureImporter: `ReadTextureImportInstructions(UnityEditor.TextureImportInstructions, UnityEditor.BuildTarget)` -> `ReadTextureImportInstructions(UnityEditor.BuildTarget, out UnityEngine.TextureFormat, out UnityEngine.ColorSpace, out System.Int32)`
- InteractiveCloth /SkinnedCloth -> Cloth (Not possible at all.)
- GameObjectUtility: `GetNavMeshLayerNames()` -> `GetNavMeshAreaNames()`
- WWW: `WWW(string, byte[], System.Collections.Hashtable)` -> `WWW(string, byte[], System.Collections.Dictionary)`
- AudioClip: `Create(string,int,int,int,bool,bool)` -> `Create(string,int,int,int,bool)`
- IPackerPolicy: `OnGroupAtlases(UnityEditor.BuildTarget, UnityEditor.Sprites.PackerJob, UnityEditor.TextureImporter[])` -> `OnGroupAtlases(UnityEditor.BuildTarget, UnityEditor.Sprites.PackerJob, System.Int32[])` (completely different param type)
- `PasteToStateMachineFromPasteboard`
- `CopyStateMachineDataToPasteboard`
- AssetBundle: `Load` (changed behaviour)
- MeshCollider: `bool smoothSphereCollisions` (removed)
- TerrainData: `PhysicMaterial physicMaterial`  (removed)