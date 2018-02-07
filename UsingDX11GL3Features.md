# DirectX 11 and OpenGL Core

Unity supports DirectX 11 (DX11) and OpenGL Core graphics APIs. This page details how to use them.

## Enabling DirectX 11

DirectX 11 is enabled by default on Windows. Your games and the Unity Editor use DX11, and fall back to DX9 when DX11 is not available. 

To enable or disable DirectX 11 for your game builds and the Editor, go to __Edit__ > __Project Settings__ > __Player__ to open the [Player Settings](class-PlayerSettings). Navigate to __Other Settings__ and un-tick __Auto Graphics API for Windows__. In the panel that appears, select __Direct3D11__ and click the minus (-) button to remove it, or click the plus (+) button and choose __Direct3D11__ from the list to add it. 

![Adding __Direct3D11__ to the __Graphics APIs for Windows__ list](../uploads/Main/UsingDX11GL3Features-AddRemove.png)

Once Direct3D11 is in the list, you can drag it up and down to define the priority in which the graphics API is selected - the Unity Editor and player defaults to the one at the top of the list, and uses each one after that as a fall back option, in order of how they are listed.

**NOTE**: DX11 requires Windows Vista or later, and at least a DX10-level GPU (preferably DX11-level). The Unity Editor window title has __&lt;DX11&gt;__ at the end when it is running in DX11 mode.


## Enabling OpenGL Core

OpenGL Core is enabled by default on Mac and Linux. Your games and the Unity Editor use OpenGL Core on these platforms.

To enable OpenGL Core on Windows and make it the default, go to __Edit__ > __Project Settings__ > __Player__ to open the [Player Settings](class-PlayerSettings). Navigate to __Other Settings__ and un-tick __Auto Graphics API for Windows__. In the panel that appears, click the plus (+) button and choose __OpenGLCore__ from the list to add it. 

![Adding __OpenGLCore__ to the __Graphics APIs for Windows__ list](../uploads/Main/UsingDX11GL3Features-AddOpenGLCore.png)

OpenGL Core has the following minimum requirements:

* Mac OS X 10.8 (OpenGL 3.2), MacOSX 10.9 (OpenGL 3.2 to 4.1)
* Windows with NVIDIA since 2006 (GeForce 8), AMD since 2006 (Radeon HD 2000), Intel since 2012 (HD 4000 / IvyBridge) (OpenGL 3.2 to OpenGL 4.5)
* Linux (OpenGL 3.2 to OpenGL 4.5)


## Compute Shaders

Compute Shaders allow you to use GPU as a parallel processor. See documentation on [Compute Shaders](ComputeShaders) for more information.

## Tessellation & Geometry Shaders

Surface Shaders have support for simple tessellation and displacement. See documentation on [Surface Shader Tessellation](SL-SurfaceShaderTessellation) for more information.

When manually writing [Shader programs](SL-ShaderPrograms), you can use the full set of DX11 Shader model 5.0 features, including Geometry, Hull and Domain Shaders.


## Surface Shaders and DX11

Some parts of the [Surface Shader](SL-SurfaceShaders) compilation pipeline do not understand DX11-specific HLSL syntax, so if you're using HLSL features like StructuredBuffers, RWTextures and other non-DX9 syntax, you need to wrap it into a DX11-only preprocessor macro. See documentation on [Platform-specific differences](SL-PlatformDifferences) for more information.

## Examples

The following screenshots show examples of what you can achieve with DirectX 11 and OpenGL Core.

![](../uploads/Main/DX11Explosion2.png)

The volumetric explosion in the above shots is rendered using raymarching, which becomes plausible with Shader Model 5.0. Moreover, as it generates and updates depth values, it becomes fully compatible with depth-based Image Effects such as Depth of Field or Motion Blur.


![](../uploads/Main/DX11Hair.png) 
The hair in the above shot is implemented via tessellation and geometry Shaders to dynamically generate and animate individual strands of hair. Shading is based on a model proposed by Kajiya-Kai that enables a more believable diffuse and specular behaviour.


![](../uploads/Main/DX11Fur.png) 
Similar to the hair technique shown in the previous image, the fur on this pair of slippers is also based on generating geometry emitted from a simple base slippers Mesh.

![](../uploads/Main/DX11Bokeh1.png) 
The blur effect in the image above (known as __Bokeh__) is based on stamping a Texture on top of very bright pixels. This creates very believable camera lens blurs, especially when used in conjunction with [HDR](HDR) rendering.


![](../uploads/Main/Bokeh2.png)
This image shows an exaggerated lens blur. This is a possible result of using the [Depth of Field](PostProcessing-DepthOfField) effect.
