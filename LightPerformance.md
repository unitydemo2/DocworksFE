# Light troubleshooting and performance

|**5.6 DRAFT ADDITION TO DOCUMENTATION** |
|:---|
|This feature has additional or changed functionality in Unity 5.6. The link below is first draft document of that addition or change. As such, the information in this document may be subject to change before final release.<br/><br/>See first draft [Light Modes](https://docs.google.com/document/d/116JvLXljfbdfllOLlyzVvWmNWpbUwcYKV16blVHuS2E/edit) documentation.|

Lights can be rendered using either of two methods: 

* __Vertex lighting__ calculates the illumination only at the vertices of meshes and interpolates the vertex values over the rest of the surface. Some lighting effects are not supported by vertex lighting but it is the cheaper of the two methods in terms of processing overhead. Also, this may be the only method available on older graphics cards. 

* __Pixel lighting__ is calculated separately at every screen pixel. While slower to render, pixel lighting does allow some effects that are not possible with vertex lighting. Normal-mapping, light cookies and realtime shadows are only rendered for pixel lights. Additionally, spotlight shapes and point light highlights look much better when rendered in pixel mode.

![Comparison of a spotlight rendered in pixel vs vertex mode](../uploads/Main/LightPixVertComp.svg) 

Lights have a big impact on rendering speed, so lighting quality must be traded off against frame rate. Since pixel lights have a much higher rendering overhead than vertex lights, Unity will only render the brightest lights at per-pixel quality and render the rest as vertex lights. The maximum number of pixel lights can be set in the [Quality Settings](class-QualitySettings) for standalone build targets.

You can favour a light to be rendered as a pixel light using its __Render Mode__ property. A light with the mode set to __Important__ will be given higher priority when deciding whether or not to render it as a pixel light. With the mode set to __Auto__ (the default), Unity will classify the light automatically based on how much a given object is affected by the light. The lights that are rendered as pixel lights are determined on an object-by-object basis.

See the page about [Optimizing Graphics Performance](OptimizingGraphicsPerformance) for further information.


##Shadow performance

Realtime shadows have quite a high rendering overhead, so you should use them sparingly. Any objects that might cast shadows must first be rendered into the shadow map and then that map will be used to render objects that might receive shadows. Enabling shadows has an even bigger impact on performance than the pixel/vertex trade-off mentioned above.

Soft shadows have a greater rendering overhead than hard shadows but this only affects the GPU and does not cause much extra CPU work.

The [Quality Settings](class-QualitySettings) include a __Shadow Distance__ value. Objects that are beyond this distance from the camera will be rendered with no shadows at all. Since the shadows on distant objects will not usually be noticed anyway, this can be a useful optimisation to reduce the number of shadows that must be rendered.

A particular issue with directional lights is that a single light can potentially illuminate the whole of a scene. This means that the shadow map will often cover a large portion of the scene at once and this makes the shadows susceptible to a problem known as "perspective aliasing". Simply put, perspective aliasing means that shadow map pixels seen close to the camera look enlarged and "chunky" compared to those farther away. Although you can just increase the shadow map resolution to reduce this effect, the result is that rendering resources are wasted for distant areas whose shadow map looked fine at the lower resolution.

A good solution to the problem is therefore to use separate shadow maps that decrease in resolution as the distance from camera increases. These separate maps are known as __cascades__. From the [Quality Settings](class-QualitySettings), you can choose zero, two or four cascades; Unity will calculate the positioning of the cascades within the camera's frustum. Note that cascades are only enabled for directional lights. See [directional light shadows](DirLightShadows) page for details.


##How the size of a shadow map is calculated

The first step in calculating the size of the map is to determine the area of the screen view that the light can illuminate. For directional lights, the whole screen can be illuminated but for spot lights and point lights, the area is the onscreen projection of the shape of the light's extent (a sphere for point lights or a cone for spot lights). The projected shape has a certain width and height in pixels on the screen; the larger of those two values is then taken as the light's "pixel size".

When the shadow map resolution is set to __High__ (from the [Quality Settings](class-QualitySettings)) the shadow map's size is calculated as follows:

* **Directional lights**: [NextPowerOfTwo](ScriptRef:Mathf.NextPowerOfTwo.html) (pixelSize * 1.9), up to a maximum of 2048.
* **Spot lights**: [NextPowerOfTwo](ScriptRef:Mathf.NextPowerOfTwo.html) (pixelSize), up to a maximum of 1024.
* **Point lights**: [NextPowerOfTwo](ScriptRef:Mathf.NextPowerOfTwo.html) (pixelSize * 0.5), up to a maximum of 512.

If the graphics card has 512MB or more video memory, the upper shadow map limits are increased to 4096 for directional lights, 2048 for spot lights and 1024 for point lights.

At _Medium_ shadow resolution, the shadow map size is half the value for __High__ resolution and for _Low_, it is a quarter of the size.

Point lights have a lower limit on size than the other types is because they use cubemaps for shadows. That means that six cubemap faces at this resolution must be kept in video memory at once. They are also quite expensive to render, as potential shadow casters might need to be rendered into all six cubemap faces. 


##Troubleshooting shadows

If you find that one or more objects are not casting shadows then you should check the following points:

* Old graphics hardware may not support shadows. See below for a list of minimal hardware specs that can handle shadows.

* Shadows can be disabled in the [Quality Settings](class-QualitySettings). Make sure that you have the correct quality level enabled and that shadows are switched on for that setting.

* All [Mesh Renderers](class-MeshRenderer) in the scene must be set up with their _Receive Shadows_ and _Cast Shadows_ correctly set. Both are enabled by default but check that they haven't been disabled unintentionally.

* Only opaque objects cast and receive shadows so objects using the built-in [Transparent](shader-TransparentFamily) or Particle shaders will neither cast nor receive. Generally, you can use the [Transparent Cutout](shader-TransparentCutoutFamily) shaders instead for objects with "gaps" such as fences, vegetation, etc. Custom [Shaders](Shaders) must be pixel-lit and use the [Geometry render queue](SL-SubShaderTags).

* Objects using __VertexLit__ shaders can't receive shadows but they can cast them.

* With the [Forward rendering path](RenderTech-ForwardRendering), some shaders allow only the brightest directional light to cast shadows (in particular, this happens with Unity's legacy built-in shaders from 4.x versions). If you want to have more than one shadow-casting light then you should use the [Deferred Shading](RenderTech-DeferredShading) rendering path instead. You can enabled your own shaders to support "full shadows" by using the `fullforwardshadows` [surface shader](SL-SurfaceShaders) directive.


##Hardware support for shadows

Built-in shadows work on almost all devices supported by Unity. The following cards are supported on each platform:

### PC (Windows/Mac/Linux)

* Generally all GPUs support shadows. Exceptions might occur in some really old GPUs (for example, Intel GPUs made in 2005).

### Mobile
* iPhone 4 does not support shadows. All later models starting with iPhone 4S and iPad 2 support shadows.
* Android: Requires Android 4.0 or later, and `GL_OES_depth_texture` support. Most notably, some Android Tegra 2/3-based Android devices do not have this, so they don't support shadows.
* Windows Phone: Shadows are only supported on DX11-class GPUs (Adreno 4xx/5xx).

### Consoles
* All consoles support shadows.
