# Low-level Native Plugin Interface

In addition to the basic script interface, [Native Code Plugins](Plugins) in Unity can receive callbacks when certain events happen. This is mostly used to implement low-level rendering in your plugin and enable it to work with Unity's multithreaded rendering.

Headers defining interfaces exposed by Unity are provided with the editor.


## Interface Registry

A plugin should export `UnityPluginLoad` and `UnityPluginUnload` functions to handle main Unity events. See `IUnityInterface.h` for the correct signatures. `IUnityInterfaces` is provided to the plugin to access further Unity APIs.

````
#include "IUnityInterface.h"
#include "IUnityGraphics.h"
// Unity plugin load event
extern "C" void UNITY_INTERFACE_EXPORT UNITY_INTERFACE_API
    UnityPluginLoad(IUnityInterfaces* unityInterfaces)
{
    IUnityGraphics* graphics = unityInterfaces->Get<IUnityGraphics>();
}
````


## Access to the Graphics Device

A plugin can access generic graphics device functionality by getting the `IUnityGraphics` interface. In earlier versions of Unity a `UnitySetGraphicsDevice` function had to be exported in order to receive notification about events on the graphics device. Starting with Unity 5.2 the new IUnityGraphics interface (found in `IUnityGraphics.h`) provides a way to register a callback.

````
#include "IUnityInterface.h"
#include "IUnityGraphics.h"
    
static IUnityInterfaces* s_UnityInterfaces = NULL;
static IUnityGraphics* s_Graphics = NULL;
static UnityGfxRenderer s_RendererType = kUnityGfxRendererNull;
    
// Unity plugin load event
extern "C" void UNITY_INTERFACE_EXPORT UNITY_INTERFACE_API
    UnityPluginLoad(IUnityInterfaces* unityInterfaces)
{
    s_UnityInterfaces = unityInterfaces;
    s_Graphics = unityInterfaces->Get<IUnityGraphics>();
        
    s_Graphics->RegisterDeviceEventCallback(OnGraphicsDeviceEvent);
        
    // Run OnGraphicsDeviceEvent(initialize) manually on plugin load
    // to not miss the event in case the graphics device is already initialized
    OnGraphicsDeviceEvent(kUnityGfxDeviceEventInitialize);
}
    
// Unity plugin unload event
extern "C" void UNITY_INTERFACE_EXPORT UNITY_INTERFACE_API
    UnityPluginUnload()
{
    s_Graphics->UnregisterDeviceEventCallback(OnGraphicsDeviceEvent);
}
    
static void UNITY_INTERFACE_API
    OnGraphicsDeviceEvent(UnityGfxDeviceEventType eventType)
{
	switch (eventType)
	{
	    case kUnityGfxDeviceEventInitialize:
		{
			s_RendererType = s_Graphics->GetRenderer();
			//TODO: user initialization code
			break;
		}
	    case kUnityGfxDeviceEventShutdown:
		{
			s_RendererType = kUnityGfxRendererNull;
			//TODO: user shutdown code
			break;
		}
    	case kUnityGfxDeviceEventBeforeReset:
		{
		    //TODO: user Direct3D 9 code
			break;
		}
    	case kUnityGfxDeviceEventAfterReset:
		{
		    //TODO: user Direct3D 9 code
			break;
		}
	};
}
````    

## Plugin Callbacks on the Rendering Thread

Rendering in Unity can be multithreaded if the platform and number of available CPUs will allow for it. When multithreaded rendering is used, the rendering API commands happen on a thread which is completely separate from the one that runs MonoBehaviour scripts. Consequently, it is not always possible for your plugin to start doing some rendering immediately, because it might interfere with whatever the render thread is doing at the time.

In order to do **any** rendering from the plugin, you should call [GL.IssuePluginEvent](ScriptRef:GL.IssuePluginEvent.html) from your script. This will cause the provided native function to be called from the render thread. For example, if you call GL.IssuePluginEvent from the camera's OnPostRender function, you get a plugin callback immediately after the camera has finished rendering.

Signature for the `UnityRenderingEvent` callback is provided in `IUnityGraphics.h`.
Native plugin code example:

````
// Plugin function to handle a specific rendering event
static void UNITY_INTERFACE_API OnRenderEvent(int eventID)
{
    //TODO: user rendering code
}
    
// Freely defined function to pass a callback to plugin-specific scripts
extern "C" UnityRenderingEvent UNITY_INTERFACE_EXPORT UNITY_INTERFACE_API
    GetRenderEventFunc()
{
    return OnRenderEvent;
}
````
    
Managed plugin code example:
    
````
#if UNITY_IPHONE && !UNITY_EDITOR
[DllImport ("__Internal")]
#else
[DllImport("RenderingPlugin")]
#endif
private static extern IntPtr GetRenderEventFunc();
	
// Queue a specific callback to be called on the render thread
GL.IssuePluginEvent(GetRenderEventFunc(), 1);
````

Such callbacks can now also be added to CommandBuffers via [CommandBuffer.IssuePluginEvent](ScriptRef:Rendering.CommandBuffer.IssuePluginEvent.html).

## Plugin using the OpenGL graphics API

There are two kind of OpenGL objects: Objects shared across OpenGL contexts (texture; buffer; renderbuffer; samplers; query; shader; and programs objects) and per-OpenGL context objects (vertex array; framebuffer; program pipeline; transform feedback; and sync objects).

Unity uses multiple OpenGL contexts. When initializing and closing the editor and the player, we rely on a **master** context but we use dedicated contexts for rendering. Hence, you can’t create per-context objects during `kUnityGfxDeviceEventInitialize` and `kUnityGfxDeviceEventShutdown` events.

For example, a native plugin can't create a vertex array object during a `kUnityGfxDeviceEventInitialize` event and use it in a `UnityRenderingEvent` callback, because the active context is not the one used during the vertex array object creation.

## Example


An example of a low-level rendering plugin is on bitbucket: **[bitbucket.org/Unity-Technologies/graphicsdemos](https://bitbucket.org/Unity-Technologies/graphicsdemos)** (NativeRenderingPlugin folder). It demonstrates two things:


* Renders a rotating triangle from C++ code after all regular rendering is done.
* Fills a procedural texture from C++ code, using Texture.GetNativeTexturePtr to access it.

The project works with:

* Windows (Visual Studio 2015) with Direct3D 9, Direct3D 11, Direct3D 12 and OpenGL.
* Mac OS X (Xcode) with Metal and OpenGL.
* Windows Store Apps (Windows 10 and Windows 8.1 flavors) with Direct3D 11 and Direct3D 12.
* WebGL

