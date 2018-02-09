# Graphics Command Buffers

It is possible to extend Unity's [rendering pipeline](SL-RenderPipeline) with so called "command buffers".
A command buffer holds list of rendering commands ("set render target, draw mesh, ..."), and can be
set to execute at various points during camera rendering.

For example, you could render some additional objects into [deferred shading](RenderTech-DeferredShading)
G-buffer after all regular objects are done.

A high-level overview of how cameras render scene in Unity is shown below. At each point
marked with a green dot, you can add command buffers to execute your commands.

![](../uploads/SL/CameraRenderFlowCmdBuffers.svg)

See [CommandBuffer scripting class](ScriptRef:Rendering.CommandBuffer.html) and
[CameraEvent enum](ScriptRef:Rendering.CameraEvent.html) for more details.

Command buffers can also be used as a replacement for, or in conjunction with [image effects](WritingImageEffects).


## Example Code

Sample project demonstrating some of the techniques possible with command buffers:
**[RenderingCommandBuffers.zip](../uploads/Examples/RenderingCommandBuffers.zip)**.

### Blurry Refractions

This scene shows a "blurry refraction" technique.

![](../uploads/Main/RenderingCommandBufferBlurryRefraction.png)

After opaque objects and skybox is rendered, current image is copied into a temporary
render target, blurred and set up a global shader property. Shader on the glass
object then samples that blurred image, with UV coordinates offset based on a normal map
to simulate refraction.

This is similar to what [shader GrabPass does](SL-GrabPass) does, except
you can do more custom things (in this case, blurring).


### Custom Area Lights in Deferred Shading

This scene shows an implementation of "custom deferred lights": sphere-shaped lights,
and tube-shaped lights.

![](../uploads/Main/RenderingCommandBufferCustomLights.png)

After regular deferred shading light pass is done,
a sphere is drawn for each custom light, with a shader that computes illumination
and adds it to the lighting buffer.


### Decals in Deferred Shading

This scene shows a basic implementation of "deferred decals".

![](../uploads/Main/RenderingCommandBufferDecals.png)

The idea is: after G-buffer is done, draw each "shape" of the decal (a box)
and modify the G-buffer contents. This is very similar to how lights are done
in deferred shading, except instead of accumulating the lighting
we modify the G-buffer textures.

![](../uploads/Main/RenderingCommandBufferDecalsScene.png)

Each decal is implemented as a box here, and affects any geometry inside the box
volume.
