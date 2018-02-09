#Publishing Builds

At any time while you are creating your game, you might want to see how it looks when you build and run it outside of the editor as a standalone. This section will explain how to access the __Build Settings__ and how to create different builds of your games.

__File-&gt;Build Settings...__ is the menu item to access the Build Settings window. It pops up an editable list of the scenes that will be included when you build your game.

![The Build Settings window](../uploads/Main/BuildSettings.png) 

The first time you view this window in a project, it will appear blank. If you build your game while this list is blank, only the currently open scene will be included in the build. If you want to quickly build a test player with only one scene file, just build a player with a blank scene list.

It is easy to add scene files to the list for multi-scene builds. There are two ways to add them. The first way is to click the __Add Open Scenes__ button. You will see the currently open scenes appear in the list. The second way to add scene files is to drag them from the __Project View__ to the list.

At this point, notice that each of your scenes has a different index value. __Scene 0__ is the first scene that will be loaded when you build the game. When you want to load a new scene, use [Application.LoadLevel()](ScriptRef:Application.LoadLevel.html) inside your scripts.

If you've added more than one scene file and want to rearrange them, simply click and drag the scenes on the list above or below others until you have them in the desired order.

If you want to remove a scene from the list, click to highlight the scene and press __Command-Delete__. The scene will disappear from the list and will not be included in the build.

When you are ready to publish your build, select a __Platform__ and make sure that the Unity logo is next to the platform; if its not then click in the __Switch Platform__ button to let Unity know which platform you want to build for. Finally press the __Build__ button. You will be able to select a name and location for the game using a standard Save dialog. When you click __Save__, Unity builds your game pronto. It's that simple. If you are unsure where to save your built game to, consider saving it into the projects root folder. You cannot save the build into the Assets folder.

Enabling the __Development Build__ checkbox on a player will enable [Profiler](ScriptRef:Profiling.Profiler.html) functionality and also make the Autoconnect Profiler and Script Debugging options available.

Further information about the Build Settings window can be found on the [Build Settings](BuildSettings) page.


##Building standalone players

With Unity you can build standalone applications for Windows, Mac and Linux. It's simply a matter of choosing the build target in the build settings dialog, and hitting the 'Build' button.
When building standalone players, the resulting files will vary depending on the build target. For the Windows build target, an executable file (.exe) will be built, along with a Data folder which contains all the resources for your application. For the Mac build target, an app bundle will be built which contains the file needed to run the application as well as the resources.

Distributing your standalone on Mac is just to provide the app bundle (everything is packed in there). On Windows you need to provide both the .exe file and the Data folder for others to run it. Think of it like this: Other people must have the same files on their computer, as the resulting files that Unity builds for you, in order to run your game.


##Inside the build process

The building process will place a blank copy of the built game application wherever you specify. Then it will work through the scene list in the build settings, open them in the editor one at a time, optimize them, and integrate them into the application package. It will also calculate all the assets that are required by the included scenes and store that data in a separate file within the application package.


* Any __GameObject__ in a scene that is tagged with 'EditorOnly' will not be included in the published build. This is useful for debugging scripts that don't need to be included in the final game.


* When a new level loads, all the objects in the previous level are destroyed. To prevent this, use [DontDestroyOnLoad()](ScriptRef:Object.DontDestroyOnLoad.html) on any objects you don't want destroyed. This is most commonly used for keeping music playing while loading a level, or for game controller scripts which keep game state and progress.


* After the loading of a new level is finished, the message: [OnLevelWasLoaded()](ScriptRef:MonoBehaviour.OnLevelWasLoaded.html) will be sent to all active game objects.
* For more information on how to best create a game with multiple scenes, for instance a main menu, a high-score screen, and actual game levels, check our [Tutorials](http://unity3d.com/learn/tutorials/modules).


##Preloading

Published builds automatically preload all assets in a scene when the scene loads. The exception to this rule is scene 0. This is because the first scene is usually a splashscreen, which you want to display as quickly as possible.

To make sure all your content is preloaded, you can create an empty scene which calls __Application.LoadLevel(1)__. In the build settings make this empty scene's index 0. All subsequent levels will be preloaded.


##You're ready to build games

By now, you have learned how to use Unity's interface, how to use assets, how to create scenes, and how to publish your builds. There is nothing stopping you from creating the game of your dreams. You'll certainly learn much more along the way, and we're here to help.

To learn more about constructing game levels, see the section on [Creating Scenes](CreatingScenes).

To learn more about Scripting, see the [Scripting Section](ScriptingSection).

To learn more about creating Art and importing assets, see [Assets Workflow](AssetWorkflow) of the manual.

To interact with the community of Unity users and developers, visit the [Unity Forums](http://forum.unity3d.com). You can ask questions, share projects, build a team, anything you want to do. Definitely visit the forums at least once, because we want to see the amazing games that you make.
