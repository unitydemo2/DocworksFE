# Using WebGL Templates

When you build a WebGL project, Unity embeds the player in an HTML page so that it can be played in the browser. The default page is a simple white page with a loading bar on a grey canvas. Alternatively, you can select a minimal template (with only the necessary boilerplate code to run the WebGL content) in the Player Settings inspector (menu: Edit > Project Settings > Player).

![](../uploads/Main/WebGLTemplate1.png)

The built-in HTML pages are fine for testing and demonstrating a minimal player but for production purposes, it is often desirable to see the player hosted in the page where it will eventually be deployed. For example, if the Unity content interacts with other elements in the page via the external call interface then it must be tested with a page that provides those interacting elements. Unity allows you to supply your own pages to host the player by using __WebGL templates__.

## Structure of a WebGL Template

Custom templates are added to a project by creating a folder called "WebGLTemplates" in the Assets folder - the templates themselves are sub-folders within this folder. Each template folder contains an *index.html* file along with any other resources the page needs, such as images or stylesheets.

![](../uploads/Main/WebGLTemplate2.png)

Once created, the template will appear among the options on the Player Settings inspector. (the name of the template will be the same as its folder). Optionally, the folder can contain a file named *thumbnail.png*, which should have dimensions of 128x128 pixels. The thumbnail image will be displayed in the inspector to hint at what the finished page will look like.

The html file needs to contain at least the following elements:

* Script tag for the Unity WebGL loader:
 `<script src="%UNITY_WEBGL_LOADER_URL%"></script>`

* Script for instantiating the game: `<script> var gameInstance = UnityLoader.instantiate("gameContainer", "%UNITY_WEBGL_BUILD_URL%");</script>`

* A `<div>` tag, which *id* is used in the instantiation function. The contents of this div will be replaced with the game instance.

## __UnityLoader.instantiate(container, url, override)__

*UnityLoader.instantiate* is responsible for creating a new instance of your content. 

* __container __can be either a DOM element (normally a `<div>` element) or an id of a DOM element. If the DOM element is provided, then the game will be instantiated immediately. If an id of a DOM element is provided, then the game will be instantiated after the whole document is parsed (which means you can provide an id of a DOM element which has not yet been created at the time of *UnityLoader.instantiate()* call).

* __url __specifies the address of the json file, which contains information about the build (you may use the *%UNITY_WEBGL_BUILD_URL%* variable which will be automatically resolved at build time).

* __override__ is an optional parameter which can be used to override the default properties of the game instance. For example you can override *onProgress *and *popup *function, as those are properties of the game instance. Note that *Module *is a property of the game instance as well, so the properties of the *Module *can be overridden at instantiation time. Consider the following example:

```
UnityLoader.instantiate("MyContainer", “build/MyBuild.json”, {
	onProgress: MyProgressFunction,
	Module: {
		TOTAL_MEMORY: 268435456,
		onRuntimeInitialized: MyInitializationCallbackFunction,
	},
});
```
## Template Tags

During the build process, Unity will look for special tag strings in the page text and replace them with values supplied by the editor. These include the name, onscreen dimensions and various other useful information about the player.

The tags are delimited by percent signs (%) in the page source. For example, if the product name is defined as "MyPlayer" in the Player settings:-

   `<title>%UNITY_WEB_NAME%</title>`

…in the template’s index file will be replaced with

   `<title>MyPlayer</title>`

…in the host page generated for the build. The complete set of tags is given below:-

* __UNITY_WEB_NAME__: Name of the player.

* __UNITY_WEBGL_LOADER_URL__: Url of the UnityLoader.js script, which performs instantiation of the build.

* __UNITY_WEBGL_BUILD_URL__: Url of the JSON file, containing all the necessary information about the build.

* __UNITY_WIDTH__ and __UNITY_HEIGHT__: Onscreen width and height of the player in pixels.

* __UNITY_CUSTOM_SOME_TAG__: If you add a tag to the index file with the form UNITY_CUSTOM_XXX, then this tag will appear in the Player Settings when your template is selected. For example, if something like 
```
<title>Unity Player | %UNITY_CUSTOM_MYTAG%</title>
``` is added to the source, the Player Settings will look like this:-

![](../uploads/Main/WebGLTemplate3.png)

The textbox next to the tag’s name contains the text that the custom tag will be replaced with during the build.

## Example

To illustrate the use of the template tags, here is the HTML source that Unity uses for its minimal WebGL template.

```
<!DOCTYPE html>
<html lang="en-us">

  <head>
	<meta charset="utf-8">
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
	<title>Unity WebGL Player | %UNITY_WEB_NAME%</title>
	<script src="%UNITY_WEBGL_LOADER_URL%"></script>
	<script>
  	var gameInstance = UnityLoader.instantiate("gameContainer", "%UNITY_WEBGL_BUILD_URL%");
	</script>
  </head>
  
  <body>
	<div id="gameContainer" style="width: %UNITY_WIDTH%px; height: %UNITY_HEIGHT%px; margin: auto"></div>
  </body>
  
</html>
```

Both minimal and default templates can be found in the Unity installation folder under Editor\Data\PlaybackEngines\WebGLSupport\BuildTools\WebGLTemplates on Windows or /PlaybackEngines/WebGLSupport/BuildTools/WebGLTemplates on Mac.

## Adding a progress bar

Unity WebGL content will automatically render a default progress bar for you when it loads. You can override the default loading bar by providing your own progress function as an additional instantiation parameter. For example:

```
var gameInstance = UnityLoader.instantiate("gameContainer", "%UNITY_WEBGL_BUILD_URL%", {onProgress: UnityProgress});
```

where `UnityProgress` is a function of 2 arguments: `gameInstance` (identifies the game instance the progressbar belongs to) and `progress` (a value from 0.0 to 1.0, providing information about the current loading progress).

For example, the progress function in the default WebGL template looks the following way:

```
var gameInstance = UnityLoader.instantiate("gameContainer", "%UNITY_WEBGL_BUILD_URL%", {onProgress: UnityProgress});
```

where UnityProgress is a function of 2 arguments: gameInstance (identifies the game instance the progressbar belongs to) and progress (a value from 0.0 to 1.0, providing information about the current loading progress).

For example, the progress function in the default WebGL template looks the following way:

```
function UnityProgress(gameInstance, progress) {
  if (!gameInstance.Module)
    return;
  if (!gameInstance.logo) {
    gameInstance.logo = document.createElement("div");
    gameInstance.logo.className = "logo " + gameInstance.Module.splashScreenStyle;
    gameInstance.container.appendChild(gameInstance.logo);
  }
  if (!gameInstance.progress) {    
    gameInstance.progress = document.createElement("div");
    gameInstance.progress.className = "progress " + gameInstance.Module.splashScreenStyle;
    gameInstance.progress.empty = document.createElement("div");
    gameInstance.progress.empty.className = "empty";
    gameInstance.progress.appendChild(gameInstance.progress.empty);
    gameInstance.progress.full = document.createElement("div");
    gameInstance.progress.full.className = "full";
    gameInstance.progress.appendChild(gameInstance.progress.full);
    gameInstance.container.appendChild(gameInstance.progress);
  }
  gameInstance.progress.full.style.width = (100 * progress) + "%";
  gameInstance.progress.empty.style.width = (100 * (1 - progress)) + "%";
  if (progress == 1)
    gameInstance.logo.style.display = gameInstance.progress.style.display = "none";
}
```

You can use it as is or as reference for your own templates. Since the progress bar is completely implemented in JavaScript, you can customize or replace it to show anything you want as a progress indication.

----
*  <span class="page-edit">2017-05-24  <!-- include IncludeTextAmendPageNoEdit --></span>

* <span class="page-history">Updated in 5.6</span>


