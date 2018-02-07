# Lighting: Technical information and terminology

* __Surface__: All triangles from all meshes in a Scene together are called the **surface** of a scene. A surface point is a point within any triangle defined for the Scene.

* __Emitted Light__: This is light that is emitted directly onto the surface of the Scene.

* __Direct Light__: This is light that is emitted, hits the surface of the Scene and is then reflected into a sensor (for example, the eye’s retina or a camera). A Light’s direct contribution is any direct light that arrives at a sensor from that Light. 

* __Indirect Light__: This is light that is emitted, hits the surface of the Scene at least two times and is ultimately reflected into a sensor. A Light’s indirect contribution is any indirect light that arrives at a sensor from that Light.

![](../uploads/Main/LightModes-TechnicalInformation-0.png)

### Reflection of simulated light in a Scene

Rough surfaces scatter incoming light in many directions, illuminating surfaces that are not directly lit from light sources. The rougher the surfaces in a scene, the brighter such shadowed areas will appear. In the past, this effect was approximated by defining one additional ambient light color which was simply added to the result of direct lighting, so that surfaces in shadows would not appear completely black. More sophisticated approximations use a gradient to simulate different ambient colors depending on the orientation of the surface, or even spherical harmonics to have even more complex [ambient lighting](GlobalIllumination).

Smooth or glossy surfaces reflect most of the incoming light in predictable directions, leading to visible highlights on materials. The extreme case of a glossy surface is a mirror, where all the incoming light from one direction gets reflected into exactly one other direction. A variation of glossy reflections are translucent materials, that can also refract incoming light when it enters and leaves the material again. 

In the case of indirect lighting, a light path has at least two interactions with the Scene’s surface. These interactions can be a combination of glossy and/or rough surface reflections. For example, glossy reflections/refractions hitting a rough surface display patterns of focused light and darkness visible from all viewing directions, which are called **caustics**. Rough reflections hitting another rough surface are usually referred to as **ambient lighting**.

Due to the nature of light being reflected multiple times on the surface of a scene, a correct solution needs to take the entire scene with all its surface material properties and light interactions for all relevant light paths into account. Hence the term [Global Illumination](GIIntro).

### Solving the problem

*Ray tracing* is a very elegant way of solving this problem in computer graphics, as it tries to simulate what actually happens in the real world by following ray paths through the scene. The movie industry has entirely moved to ray tracing at this point for generating their images. 

Unfortunately, ray tracing is still too slow to be used in most real time graphics, where [rasterization](https://en.wikipedia.org/wiki/Rasterisation) is the standard method of generating images. Unlike ray tracing, rasterization cannot follow arbitrary light paths through the scene. In fact, a rasterizer can only ever calculate one segment of a light path. This is why lighting in real time graphics gets complicated.

Since rasterizers cannot follow light rays, real time lighting concentrates on the parts of lighting with the most visible impact. These are emission, and more commonly, direct lighting. Even in this case the light path already consists of two segments - one from the camera to the surface, and one from the surface to the light. 

The first segment is the view rendered from the camera position. In order to calculate the second segment, techniques like [shadow mapping](Shadows) are used. Since shadow maps are specific to each shadow-casting Light, a unique shadow map must be generated for each one. The more shadow-casting Lights there are, the more shadow maps need to be generated. Depending on the number of Lights there are, required rendering time can quickly become too long. Another drawback of shadow maps is their limited resolution.  This leads to blocky shadows. Therefore, shadow maps present both an image quality issue due to the limited resolution, and a performance issue due to the memory requirements to store the shadow maps and the time it takes to generate them every frame. 

Unlike offline rendering, games have certain hard limits on how much time they can spend rendering a frame. For instance, VR applications have 11.11 milliseconds to draw a frame, in order to achieve 90 frames per second (FPS). Games relying on fast player reactions have 16.66ms to draw a frame in order to hit 60 FPS. Games that target 30 FPS have 33.33ms. These times must also include calculations for the rest of the application or game, such as AI and physics. It is therefore important to make everything as efficient as possible to get the most out of the system. All rendering must occur within less than the time between frames.

### Summary

To recap, the two major issues that need to be addressed are:

1. How to deal with the performance penalty caused by calculating shadows for direct lighting.

2. How to deal with indirect lighting (note: in the context of real time graphics, Global Illumination is synonymous with indirect lighting, even though the actual meaning encompasses direct lighting as well).

---

* <span class="page-edit"> 2017-06-08  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Light Modes added in 5.6</span>
