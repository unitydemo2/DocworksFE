# Asynchronous compute

Unity provides an API interface for asynchronous compute (also called "async compute"). Async compute allows you to use GPU resources more efficiently when performing compute shader tasks. It is especially useful if you are issuing custom compute shader dispatches.

This page is split into two sections:

* [Introduction to async compute](#AsyncComputeIntro)

* [Using async compute in Unity](#AsyncComputeUsing)

**Note:** Only PS4 development supports async compute.

<a name="AsyncComputeIntro"></a>

## Introduction to async compute

The modern rendering pipeline does not always make use of the full capacity of the GPU. Getting the most efficient use from the available compute units can be a challenge, but is a key factor in getting good GPU performance from complex Scenes. 

Under-utilizing the compute units often occurs during depth-only rendering, such as shadow map creation or depth prepasses. During these stages, there is often no pixel shader bound to the GPU, and the GPU cannot create vertex shader wavefronts fast enough to fully make use of all the wavefronts the hardware has to offer. As a result, the rendering process is not making use of the GPU’s full computational power. 

Consider a GPU that has ten wavefronts available per single-instruction, multiple data (SIMD) unit. The wavefront distribution on a single SIMD unit is loosely represented in the diagram below: 

![](../uploads/Main/AsyncCompute-0.png)

In this scenario, the GPU carries out four steps:

1. Performs some vertex and pixel shader rendering

2. Switches to perform depth-only work

3. Performs some work using the compute shaders

4. Switches back to vertex and pixel shader draws 

Asynchronous compute allows you to schedule compute shader work on __compute queues__ to run simultaneously alongside tasks scheduled from the __graphics queue__. This makes efficient use of GPU resources that the rendering process is not using.

In the example described above, you could schedule custom compute shader dispatches on one or more compute queue to run at the same time as the depth-only rendering on the graphics queue. These compute shader dispatches make good use of the computational resources of the GPU, which the depth-only pass does not use. 

The diagram below shows the same scenario as the first diagram, but with async compute applied:

![](../uploads/Main/AsyncCompute-1.png)

By comparing the two diagrams, you can see that:

* With async compute, the time it takes to complete the compute processing is longer than if it was dispatched on the graphics queue. However, async compute reduces the overall time it takes to complete all of the work, which can improve performance.

* Moving the compute work to coincide with either of the two vertex and pixel shader-enabled draw operations might not enhance optimization, because all wavefronts are in use at that time. However, you can improve performance by pairing async compute operations that have different bottlenecks with tasks running on the graphics queue (for example, ALU and bandwidth). For optimum performance improvement, use trial and error to determine where async compute operations can overlap with graphics queue tasks.

<a name="AsyncComputeUsing"></a>

## Using async compute in Unity

For best results, use Unity’s async compute scripting interface as part of a [scriptable render pipeline](ScriptableRenderPipeline). This provides the most flexibility for scheduling async compute work relative to the graphics queue. You can also use async compute in projects that do not use scriptable render pipelines.

Use a graphics [command buffer](GraphicsCommandBuffers) interface to issue work to the async compute queues. To do this, construct a command buffer containing only compute queue-compatible work, then use [Graphics.ExecuteCommandBufferAsync](ScriptRef:Graphics.ExecuteCommandBufferAsync.html)or [ScriptableRenderContext.ExecuteCommandBufferAsync](ScriptRef:Experimental.Rendering.ScriptableRenderContext.ExecuteCommandBufferAsync.html) to submit it. All of the commands within the submitted buffer execute on the same compute queue. 

The following commands are valid within command buffers for async compute execution. If you attempt to asynchronously execute command buffers that contain any command not included below, you generate an error that appears in the Unity Editor and in the log at runtime:

* [CopyCounterValue](ScriptRef:Rendering.CommandBuffer.CopyCounterValue.html)

* [CopyTexture](ScriptRef:Rendering.CommandBuffer.CopyTexture.html)

* [CreateGPUFence](ScriptRef:Rendering.CommandBuffer.CreateGPUFence.html)

* [DispatchCompute](ScriptRef:Rendering.CommandBuffer.DispatchCompute.html)

* [WaitOnGPUFence](ScriptRef:Rendering.CommandBuffer.WaitOnGPUFence.html)

* Any of the `SetCompute[...]Param` commands ([SetComputeBufferParam](ScriptRef:Rendering.CommandBuffer.SetComputeBufferParam.html), [SetComputeFloatParam](ScriptRef:Rendering.CommandBuffer.SetComputeFloatParam.html), [SetComputeFloatParams](ScriptRef:Rendering.CommandBuffer.SetComputeFloatParams.html), [SetComputeIntParam](ScriptRef:Rendering.CommandBuffer.SetComputeIntParam.html), [SetComputeIntParams](ScriptRef:Rendering.CommandBuffer.SetComputeIntParams.html), [SetComputeTextureParam](ScriptRef:Rendering.CommandBuffer.SetComputeTextureParam.html), [SetComputeVectorParam](ScriptRef:Rendering.CommandBuffer.SetComputeVectorParam.html))

If you execute command buffers asynchronously on platforms that do not support async compute, Unity submits the work to the graphics queue. Use [SystemInfo.supportsAsyncCompute](ScriptRef:SystemInfo-supportsAsyncCompute.html) to check support for async compute on a given platform.

To schedule work related to graphics tasks, use [GPUFences](ScriptRef:Rendering.GPUFence.html). The rendering pipeline passes these fences when the last `Blit`, `Clear`, `Draw`, `Dispatch` or `Copy` operation issued by Unity’s graphics processing has completed on the GPU, either as a result of a graphics-related command issued from your script, or from Unity’s own internal processing to render the Scene. You can use [Graphics.CreateGPUFence](ScriptRef:Graphics.CreateGPUFence.html)or [CommandBuffer.CreateGPUFence](ScriptRef:Rendering.CommandBuffer.CreateGPUFence.html) to create GPU fences. 

Use [Graphics.WaitOnGPUFence](ScriptRef:Graphics.WaitOnGPUFence.html) to make the GPU’s graphics queue or an async compute queue wait for the rendering pipeline to pass a given fence before proceeding. Use [CommandBuffer.WaitOnGPUFence](ScriptRef:Rendering.CommandBuffer.WaitOnGPUFence.html) to make an async compute queue wait for the rendering pipeline to pass a given fence before proceeding. Neither of these functions stalls the CPU.

To ensure optimal use of GPU resources, think about when to start async compute work relative to work on the graphics queue. Most async compute command buffers have `WaitOnGPUFence` as their first entry. If you asynchronously execute command buffers that do not wait on a fence created from the graphics queue, those command buffers execute on the GPU at an undefined point during that frame’s GPU processing, which might occur before any graphics queue work.

---

* <span class="page-edit"> 2017-11-13  <!-- include IncludeTextNewPageYesEdit --></span>

* <span class="page-history">New feature in [2017.3](https://docs.unity3d.com/2017.3/Documentation/Manual/30_search.html?q=newin20173) <span class="search-words">NewIn20173</span></span>

