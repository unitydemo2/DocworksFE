# PS4 basic profiling with Razor CPU

## Introduction

__Razor for PS4__ is a profiling tool that is part of the PS4 SDK. It exists in two forms: __Razor CPU__ for overview and CPU-related profiling, and __Razor GPU__ for detailed GPU profiling. These tools are invaluable for investigating performance issues. This document covers __Razor CPU__.

On a PS4 SDK installation with default paths, Razor is located at:

* __Razor CPU__: _C:\Program Files (x86)\SCE\ORBIS\Tools\Razor\binx64\orbis-razorx64.exe_
* __Razor GPU__: _C:\Program Files (x86)\SCE\ORBIS\Tools\New Razor GPU\bin\PS4RazorGPU.exe_

While the [Unity Profiler](https://docs.unity3d.com/Manual/Profiler.html) can be used to see where time is being spent and investigate performance, framerate and glitch issues, Razor provides more detailed information that helps when improving performance.

## Getting started

Razor is used for two main activities: finding general framerate problems, and finding specific short-lived spikes or glitches.

For general framerate investigations, the first step is to use __Razor CPU__ to establish whether your game is CPU-bound or GPU-bound. The difference is as follows:

* __CPU-bound__: Framerate is being dictated by the work done on the CPU. This could be script work in fixed, general or late update, or the CPU side costs of animation, draw calls and physics work. Note in particular that a title *can *be CPU-bound on rendering work (draw calls in particular). This is where Razor can provide more detail: just because the Unity profiler suggests a high load in rendering, it may not mean the title is actually GPU-bound.

* __GPU-bound__: Framerate is being dictated by the workload on the GPU. This could be Shader cost, Image Effects, or complex geometry (very large numbers of polygons).

If your game is CPU-bound, then altering Shaders, reducing poly counts, Textures and using cheaper Image Effects has no effect on your framerate. Likewise, optimising script code doesn't make any difference when your game is GPU-bound. It is therefore very important that you establish where to start with your optimizations. It is also sometimes useful to know where you have opportunity. For example, if your title is running at an acceptable framerate but CPU activity far exceeds GPU activity, then you might consider adding GPU work (such as Image Effects) without any impact on the frame rate.

Razor offers a number of different types of profiling captures, and the SDK documentation describes these in great detail. The most basic capture, and the best one to start with, is the __Concurrency Capture__, which shows core usage and thread activity. Razor's __Timeline__ view also allows you to see the standard Unity profiling markers in this type of capture; however, you can only see these in a Development build.

To grab a Razor __Concurrency Capture__, run a Development build of your game on the devkit and launch __Razor CPU__. Go to __Capture__ > __CPU Trace With Options__ and select __Concurrency Capture,__ with all other options left at default. Press __Capture__ to start. Press __Stop__ after you have sampled what you're interested in. Razor will then process the data and show you the information.

The initial __Summary__ page shows a Hardware Utilization graphic. This is the best way to quickly establish whether your title is CPU- or GPU-bound. Here is an example:

![](../uploads/Main/PS4ProfilingWithRazor1.png)

The leftmost column is the GPU workload - here it is at 24% of the total frame time averaged over the highlighted area of capture. The bars to the right of the vertical line 0-7 are the CPU cores; blue shading indicates user work, and orange indicates OS work. In this case, the title is CPU-bound on __Core 0__, which is the Unity Main Thread. Doing a lot more GPU work would not affect the frame rate. Conversely, to improve the frame rate, it is necessary to focus on the CPU workload on the main thread (Core 0) - script code, for example, runs on this core.

Unity’s CPU core usage looks like this:

* __Core 0__ (Main Thread): scripts, scheduling jobs

* __Core 1__ (Render Thread): takes Unity draw commands and issues native GPU instructions

* __Cores 2-6__: all other threads, including jobs, FMOD and mono threads. Note that core 6 is shared with the OS, hence the blue and orange shaded areas in the picture above.

Here's a capture showing a GPU-bound situation:

![](../uploads/Main/PS4ProfilingWithRazor2.png)

The frame rate is being governed by GPU activity. Optimizing script code, for example, has no effect on frame rate. __Razor GPU__ can then be used to get more information. To reiterate, once you know whether your frame rate is down to CPU or GPU workload, you can make decisions about where to spend time optimizing.

## Glitches and spikes

A __Concurrency Capture__ can also be used for finding the cause of short term spikes or glitches. Perform a capture as above and look at the __Frame Summary__ section, at the summary page. Here is an example:

![](../uploads/Main/PS4ProfilingWithRazor3.png)

Here you can see that the capture caught 30 frames and while most were in the 30 something ms range, two frames were much slower taking over 200ms. These were frames 23 and 18. On the table on the right, click on the frame you're interested in to jump to the Timeline view and show what was going on during that frame. 

## Timeline view

You can switch Razor into a __Timeline__ view where all captured frames are available and the Unity profiler markers can be seen (in a development build). Be sure to try this out when learning to use Razor to investigate performance. It is selectable in the __Current View__ drop down box. 

For spikes, use the __Timeline__ to see where exceptional time is spent and investigate issues. There should be some stand-out remarkable difference between slow frames and the regular ones. Use that information to improve the spikes.

Here is an example of a spike in Main Thread in the __Timeline__ view, in a Development build:

![](../uploads/Main/PS4ProfilingWithRazor4.png)

The view is zoomed to show data for two frames: frame #313 at left, and frame #314 at right. At the top of the view, over the green background, you can see that frame #313 had a duration of 6.422ms, which is an average frame for this example project. However frame #314 is a spike frame with a duration of just over 16ms.

Below it, there is an area showing usage of each CPU core over time, represented with blue bars. You can see CPU 0 is almost always fully utilized, suggesting that something running on Unity's main thread produced the spike.

Further down, you can see the profiler markers, shown as purple bars. It’s often the case that you can find the cause of a spike by comparing the length of those bars, one frame against the other. In this example, the bar lengths are very similar, except for the one labeled "Update My World", which at the same time makes its parent markers, "BehaviourUpdate" and "MainLoop", much longer. This allows you to conclude that code inside the "Update My World" marker is causing the spike. This marker is in fact a user marker added in script code (using [Profiler.BeginSample](https://docs.unity3d.com/ScriptReference/Profiler.BeginSample.html)) inside a Update call in a script, which is why it’s inside Unity’s "BehaviourUpdate" marker. Using User Markers is a good way to investigate where time is being spent in your scripts.

## Summary

* Use __Razor CPU__ to get an overview and establish whether your game is CPU or GPU-bound

* Use __Razor CPU__ to investigate glitches and spikes

* Razor is best used on a development build where Unity profile markers will be visible in the Timeline view.

* A non-development build is slightly faster, so for the most accurate general framerate assessment, use a non-development build for final testing. Note that even here, there is a slight overhead in using Razor.

* If you create your own threads, particularly native threads, __Razor CPU__ allows you to investigate possible conflicts with Unity runtime activity including seeing affinity, priority and core assignment for all threads in the timeline view.

* Profile often throughout development so you keep on top of performance.

To get the most from Razor it is essential to use the SDK documentation. While a quick overview can be obtained from the information above, __Razor CPU__ and __Razor GPU__ are very powerful tools with a lot of options. The more time spent learning those options, the better informed you will be about your game’s performance. Find more information in the [Razor CPU User's Guide](https://ps4.scedev.net/resources/documents/SDK/latest/Razor_CPU-Users_Guide/__document_toc.html) and the [Razor GPU User's Guide](https://ps4.scedev.net/resources/documents/SDK/latest/Razor_GPU-Users_Guide/__document_toc.html).