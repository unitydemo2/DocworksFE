#Low-level native plugin Shader compiler access

On top of the [low-level native plugin interface](NativePluginInterface), Unity also supports low level access to the shader compiler, allowing the user to inject different variants into a shader. It is also an event driven approach in which the plugin will receive callbacks when certain builtin events happen.

The shader compiler access extension definition exposed by Unity is to be found in IUnityShaderCompilerAccess.h and it’s provided with the editor.

These extensions are supported for now only on D3D11. Support for more platforms will follow.

##Shader compiler access extension API

In order to take advantage of the rendering extension, a plugin should export UnityShaderCompilerExtEvent. There is a lot of documentation provided inside the include file.

A plugin will get called via UnityShaderCompilerExtEvent whenever one of the builtin events is triggered by Unity. The callbacks can also be added to CommandBuffers via CommandBuffer.IssuePluginEventAndData or CommandBuffer.IssuePluginCustomBlit command from scripts.

In addition to the basic script interface, [Native Code Plugins](Plugins) in Unity can receive callbacks when certain events happen. This is mostly used to implement low-level rendering in your plugin and enable it to work with Unity’s multithreaded rendering.

Headers defining interfaces exposed by Unity are provided with the editor.

##Shader compiler access configuration interface

Unity provides an interface (IUnityShaderCompilerExtPluginConfigure) to which the shader compiler access is configured. This interface is used by the plugin to reserve its own keyword(s) and configure shader program and gpu program compiler masks ( For what types for shader or GPU programs the plugin should be invoked )

---
 
* <span class="page-history">New feature in Unity [2017.1](https://docs.unity3d.com/2017.1/Documentation/Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>

* <span class="page-edit">2017-07-04 <!-- include IncludeTextNewPageNoEdit --></span>
