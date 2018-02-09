#Using WebGL Templates

When you build a WebGL project, Unity embeds the player in an HTML page so that it can be played in the browser. The default page is a simple white page with a loading bar on a grey canvas. Alternatively, you can select a minimal template (with only the necessary boilerplate code to run the WebGL content) in the Player Settings inspector (menu: Edit &gt; Project Settings &gt; Player).

![](../uploads/Main/WebGLPlayerSettings.png) 

The built-in HTML pages are fine for testing and demonstrating a minimal player but for production purposes, it is often desirable to see the player hosted in the page where it will eventually be deployed. For example, if the Unity content interacts with other elements in the page via the external call interface then it must be tested with a page that provides those interacting elements. Unity allows you to supply your own pages to host the player by using **WebGL templates**.


##Structure of a WebGL Template

Custom templates are added to a project by creating a folder called "WebGLTemplates" in the Assets folder - the templates themselves are sub-folders within this folder. Each template folder contains an _index.html_ file along with any other resources the page needs, such as images or stylesheets.

![](../uploads/Main/WebGLTemplatesProjPanel.png)

Once created, the template will appear among the options on the Player Settings inspector. (the name of the template will be the same as its folder). Optionally, the folder can contain a file named _thumbnail.png_, which should have dimensions of 128x128 pixels. The thumbnail image will be displayed in the inspector to hint at what the finished page will look like.

The html file needs to contain a canvas element with the id "canvas". Then you must insert the **UNITY\_WEBGL\_LOADER\_GLUE** tag, which will generate the required script tags to embed the Unity content, which will then render to that canvas element.

##Template Tags

During the build process, Unity will look for special tag strings in the page text and replace them with values supplied by the editor. These include the name, onscreen dimensions and various other useful information about the player.

The tags are delimited by percent signs (%) in the page source. For example, if the product name is defined as "MyPlayer" in the Player settings:-

````
	<title>%UNITY_WEB_NAME%</title>
````

...in the template's index file will be replaced with

````
	<title>MyPlayer</title>
````

...in the host page generated for the build. The complete set of tags is given below:-


* **UNITY\_WEB\_NAME**: Name of the player.

* **UNITY\_WEBGL\_LOADER\_GLUE**: This will inject the necessary script tags to embed the WebGL content. This is required to be in the template's _index.html_ file.

* **UNITY\_WIDTH** and **UNITY\_HEIGHT**: Onscreen width and height of the player in pixels.

* **UNITY\_DEVELOPMENT\_PLAYER**: 1 when building a development player, 0 otherwise.

* **UNITY\_CUSTOM\_SOME\_TAG**: If you add a tag to the index file with the form UNITY\_CUSTOM\_XXX, then this tag will appear in the Player Settings when your template is selected. For example, if something like

````
	<title>Unity Player | %UNITY_CUSTOM_MYTAG%</title>
````

...is added to the source, the Player Settings will look like this:-

![](../uploads/Main/WebGLPlayerSettingsCustomTag.png) 


The textbox next to the tag's name contains the text that the custom tag will be replaced with during the build.


##Example

To illustrate the use of the template tags, here is the HTML source that Unity uses for its minimal WebGL template.


````
<!doctype html>
<html lang="en-us">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    <title>Unity WebGL Player | %UNITY_WEB_NAME%</title>
    <link rel="stylesheet" href="TemplateData/style.css">
    <link rel="shortcut icon" href="TemplateData/favicon.ico" />
    <script src="TemplateData/UnityProgress.js"></script>
  </head>
  <body class="template">
    <p class="header"><span>Unity WebGL Player | </span>%UNITY_WEB_NAME%</p>
    <div class="template-wrap clear">
    <canvas class="emscripten" id="canvas" oncontextmenu="event.preventDefault()" height="%UNITY_HEIGHT%px" width="%UNITY_WIDTH%px"></canvas>
      <div class="logo"></div>
      <div class="fullscreen"><img src="TemplateData/fullscreen.png" width="38" height="38" alt="Fullscreen" title="Fullscreen" onclick="SetFullscreen(1);" /></div>
      <div class="title">%UNITY_WEB_NAME%</div>
    </div>
    <p class="footer">&laquo; created with <a href="http://unity3d.com/" title="Go to unity3d.com">Unity</a> &raquo;</p>
    %UNITY_WEBGL_LOADER_GLUE%
  </body>
</html>

````

##Adding a progress bar

Unity WebGL content will not automatically render a progress bar for you when it loads - the template needs to handle that. The default template included in Unity contains a _UnityProgress.js_ file which implements a simple progress bar. You can reuse that for your own templates, or use it as a reference for creating your own. Since the progress bar is completely implemented in JavaScript, you can completely customize or replace it to show anything you want as a progress indication.
