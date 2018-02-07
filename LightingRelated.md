#Related topics

Unity's lighting system is affected by and can affect many of its other effects and systems.

##Quality settings
The [Quality settings](class-QualitySettings) window has many settings that affects lighting and shadows.

##Player settings
The [Unity Player settings](class-PlayerSettings) window allows you to choose the rendering path and color space.

##Camera inspector
The [Camera inspector](class-Camera) allows you to override Unity Player settings for the rendering path per camera. HDR can also be activated here.

##Rendering paths
Unity supports a number of rendering techniques, or ‘paths’. An important early decision which needs to be made when starting a project is which path to use. Unity’s default is 'Forward Rendering”.

In Forward Rendering, each object is rendered in a ‘pass’ for each light that affects it. Therefore each object might be rendered multiple times depending upon how many lights are within range.

The advantages of this approach is that it can be very fast - meaning hardware requirements are lower than alternatives. Additionally, Forward Rendering offers us a wide range of custom ‘shading models’ and can handle transparency quickly. It also allows for the use of hardware techniques like ‘multi-sample anti-aliasing’ (MSAA) which are not available in other alternatives, such as Deferred Rendering which can have a great impact on image quality.

However, a significant disadvantage of the forward path is that we have to pay a render cost on a per-light basis. That is to say, the more lights affecting each object, the slower rendering performance will become. For some game types, with lots of lights, this may therefore be prohibitive. However if it is possible to manage light counts in your game, Forward Rendering can actually be a very fast solution.

In 'Deferred' rendering, on the other hand, we defer the shading and blending of light information until after a first pass over the screen where positions, normals, and materials for each surface are rendered to a ‘geometry buffer’ (G-buffer) as a series of screen-space textures. We then composite these results together with the lighting pass. This approach has the principle advantage that the render cost of lighting is proportional to the number of pixels that the light illuminates, instead of the number of lights themselves. As a result you are no longer bound by the number of lights you wish to render on screen, and for some games this is a critical advantage.

Deferred Rendering gives highly predictable performance characteristics, but generally requires more powerful hardware. It is also not supported by certain mobile hardware.

For more information on the Deferred, Forward and the other available rendering paths, please see the [main documentation page](RenderingPaths).

##High dynamic range
High dynamic range rendering allows you to simulate a much wider range of colours than has been traditionally available. In turn, this usually means you need to choose a range of brightnesses to display on the screen. In this way it is possible to simulate great differences in brightness between, say, outdoor lighting in our scenes and shaded areas. We can also create effects like ‘blooms’ or glows by applying effects to these bright colors in your scene. Special effects like these can add realism to particles or other visible light sources.

For more information about HDR, please see the relevant [manual page](HDR).

##Tonemapping

Tonemapping is part of the color grading [post-processing effect](PostProcessingOverview) that is required to describe how to map colours from HDR to what you can see on the screen. Please see the [Color Grading](PostProcessing-ColorGrading.html) effect for more information.

##Reflection

While not explicitly a lighting effect, reflections are important for realistically displaying materials that reflect light, such as shiny metals or glass. Modern shading techniques, including Unity's Standard Shader, integrate reflection into a material's properties.

For more information, please refer to our [section on Reflections](ReflectionProbes).

##Linear color space

In addition to selecting a rendering path, it’s important to choose a ‘Color Space’ before lighting your project. Color Space determines the maths used by Unity when mixing colors in lighting calculations or reading values from textures. This can have a drastic effect on the realism of your game, but in many cases the decision over which Color Space to use will likely be forced by the hardware limitations of your target platform.

The preferred Color Space for realistic rendering is Linear.

A significant advantage of using Linear space is that the colors supplied to shaders within your scene will brighten linearly as light intensities increase. With the alternative, ‘Gamma’ Color Space, brightness will quickly begin to turn to white as values go up, which is detrimental to image quality.

For further information please see [Linear rendering](LinearLighting).