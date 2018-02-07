Windows Phone 8: Deployment
===========================


To deploy Windows Phone 8 app on your phone follow these steps:


* Open Build Settings.
* Optionally check Development Build if you want to profile your game.
* Make sure phone is connected to PC and is unlocked.
* Click Build And Run.
* Select folder to build Visual Studio project to.
* Once the project is built and app is deployed to your phone it should appear on the screen.

This is the fastest way to deploy your app. However you might want to modify exported Visual Studio project first. In that case do the following:


* Click Build instead of Build and Run.
* Select folder to build Visual Studio project to.
* Open generated Visual Studio solution.
* Modify project if needed.
* Select desired build configuration.
* Build and deploy project to your phone.

There are three build configurations you can choose from. Debug should be used to debug your scripts. Release optimizes code for better performance. Master configuration build should be used to submit your app to the Store. It has profiler support stripped out.

Unity will not overwrite changes made to Visual Studio project.

Build Settings window has Development Build checkbox that selects Release configuration instead of Master in case build and run is clicked. Otherwise configuration can be freely chosen from Visual Studio. Additionally Development Build checkbox enables development build. In that case [Debug.isDebugBuild](ScriptRef:Debug-isDebugBuild.html) will be enabled.
