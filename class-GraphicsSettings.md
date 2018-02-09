# Graphics Settings

![](../uploads/Main/GraphicsSettings.png) 

### Scriptable RenderLoop settings

This is an experimental setting which allows you to define a series of commands to control exactly how the Scene should be rendered (instead of using the default rendering pipeline used by Unity). For more information on this experimental feature, see the Scriptable Render Pipeline documentation on GitHub.

### Camera settings

These properties control various rendering settings.

|**Setting:** |**Description:** |
|:---|:---|
|**Transparancy Sort Mode**| Renderers in Unity are sorted by several criteria such as their layer number, or their distance from camera. Transparency Sort Mode adds the ability to order renderable objects by their distance along a specific axis. This is generally only useful in 2D development; for example, sorting Sprites by height or along the Y axis.|
|Default| Sorts objects based on the Camera mode. |
|Perspective| Sorts objects based on perspective view.|
|Orthographic| Sorts objects based on orthographic view. |
|**Transparancy Sort Axis**| Use this to set a custom Transparency Sort Mode.|


### Tier settings
These settings allow you to make platform-specific adjustments to rendering and shader compilation, by tweaking builtin defines. For example, you can use this to enable Cascaded Shadows on high-tier iOS devices, but to disable them on low-tier devices to improve performance. Tiers are defined by [Rendering.GraphicsTier](ScriptRef:Rendering.GraphicsTier.html).


### Built-in shader settings


Use these settings to specify which shader is used to do lighting pass calculations in each rendering path listed.

|**Shader:** |**Calculation:** |
|:---|:---|
|__Deferred__|Used when using Deferred lighting, see [Camera: Rendering Path)(class-Camera) | 
|__Deferred Reflection__|Used when using Deferred reflection (ie reflection probes) along deferred lighting, see [Camera: Rendering Path)(class-Camera_) | 
|__Screen Space shadows__|Used when using screen space shadow.| 
|__Legacy deferred__|Used when using Legacy deferred lighting, see [Camera: Rendering Path)(class-Camera).| 
|__Motion vectors__|Used when using Legacy deferred lighting,. seem [MeshRenderer::Motion Vectors](class-MeshRenderer).| 

|**Setting:** |**Description:** |
|:---|:---|
|__Built-in shader__ (Default value)| Use Unity's built-in shaders to do the calculation. |
|__Custom shader__| Use your own compatible shader to do the calculation. This enables you to do deep customization of deferred rendering. |
|__No Support__| Disable this calculation. Use this setting if you are not using deferred shading or lighting. This will save some space in the built game data files. |

### Always-included Shaders

Specify a list of [Shaders](class-Shader) that will always be stored along with the project, even if nothing in your scenes actually uses them. It is important to add shaders used by streamed AssetBundles to this list to ensure they can be accessed.

### Shader stripping - Lightmap modes and Fog modes

Lower your build data size and improve loading times by stripping out certain shaders involved with lighting and fog.

|**_Setting:_** |**_Description:_** |
|:---|:---|
|__Automatic__ (Default value)| Unity looks at your scenes and lightmapping settings to figure out which fog and lightmapping modes are not in use, and skips corresponding shader variants. |
|__Manual__| Specify which modes to use yourself. Select this if you are [building asset bundles](BuildingAssetBundles) or changing fog modes from a script at runtime, to ensure that the modes you want to use are included. |

### Shader stripping - Instancing variants

|**_Setting:_** |**_Description:_** |
|:---|:---|
|__Strip Unused__ (Default value)| When a project is built, Unity only includes instancing shader variants if at least one material referencing the shader has the "Enable instancing" checkbox ticked. Unity strips any shaders that are not referenced by materials with the "Enable instancing" checkbox ticked.  |
|__Strip All__| Strip all instancing shader variants, even if they are being used.|
|__Keep All__| Keep all instancing shader variants, even if they are not being used.|

See [GPU instancing](GPUInstancing) for more information about Instancing variants.

### Shader preloading

Specify a list of shader variant collection assets to preload while loading the game. See [Optimizing Shader Load Time](OptimizingShaderLoadTime) page for details.


## See also

* [Optimizing Shader Load Time](OptimizingShaderLoadTime)
* [Optimizing Graphics Performance](OptimizingGraphicsPerformance)
* [Shaders reference](SL-Shader)

----

* <span class="page-edit">17-05-08 <!-- include IncludeTextAmendPageNoEdit --></span>

* <span class="page-history">New features added in 5.6</span><br/>

