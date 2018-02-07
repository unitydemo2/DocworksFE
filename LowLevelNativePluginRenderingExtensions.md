#Low-level native plugin rendering extensions

On top of the [low-level native plugin interface](NativePluginInterface), Unity also supports low level rendering extensions that can receive callbacks when certain events happen. This is mostly used to implement and control low-level rendering in your plugin and enable it to work with Unity’s multithreaded rendering.

Due to the low-level nature of this extension the plugin might need to be preloaded before the devices get created. Currently the convention is name-based namely the plugin name must be prefixed by “GfxPlugin”. Example: GfxPluginMyFancyNativePlugin.

The rendering extension definition exposed by Unity is to be found in IUnityRenderingExtensions.h and it’s provided with the editor.

These extensions are supported on all platforms supporting native plugins.

##Rendering extensions API

In order to take advantage of the rendering extension, a plugin should export UnityRenderingExtEvent and optionally UnityRenderingExtQuery. There is a lot of documentation provided inside the include file.

##Plugin callbacks on the rendering thread

A plugin will get called via UnityRenderingExtEvent whenever one of the builtin events is triggered by Unity. The callbacks can also be added to CommandBuffers via CommandBuffer.IssuePluginEventAndData or CommandBuffer.IssuePluginCustomBlit command from scripts.

-----

* <span class="page-history">New feature in Unity [2017.1](https://docs.unity3d.com/2017.1/Documentation/Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>

* <span class="page-edit">2017-07-04 <!-- include IncludeTextNewPageNoEdit --></span>
