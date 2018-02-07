# Mesh Renderer

The Mesh Renderer takes the geometry from the [Mesh Filter](class-MeshFilter) and renders it at the position defined by the object’s [Transform](class-Transform) component.

![](../uploads/Main/class-MeshRenderer-0.png)

The Mesh Renderer GameObject Component as displayed in the Inspector window

## __Properties__

| **Property:** | **Function:** |
|:---|:---| 
| __Light Probes__| Probe-based lighting interpolation mode. |
|&nbsp;&nbsp;&nbsp;&nbsp;Off:| The Renderer doesn’t use any interpolated Light Probes. |
|&nbsp;&nbsp;&nbsp;&nbsp;Blend Probes| The Renderer uses one interpolated Light Probe. This is the default option. |
|&nbsp;&nbsp;&nbsp;&nbsp;Use Proxy Volume| The Renderer uses a 3D grid of interpolated Light Probes. |
| __Reflection Probes__| Specifies how the object is affected by reflections in the scene. You cannot disable this property in deferred rendering modes.|
|&nbsp;&nbsp;&nbsp;&nbsp;Off| Reflection probes are disabled, skybox will be used for reflection. |
|&nbsp;&nbsp;&nbsp;&nbsp;Blend Probes| Reflection probes are enabled. Blending occurs only between probes, useful in indoor environments. The renderer will use default reflection if there are no reflection probes nearby, but no blending between default reflection and probe will occur. |
|&nbsp;&nbsp;&nbsp;&nbsp;Blend Probes and Skybox| Reflection probes are enabled. Blending occurs between probes or probes and default reflection, useful for outdoor environments. |
|&nbsp;&nbsp;&nbsp;&nbsp;Simple| Reflection probes are enabled, but no blending will occur between probes when there are two overlapping volumes. |
| __Anchor Override__| A Transform used to determine the interpolation position when the [Light Probe](https://docs.unity3d.com/Manual/LightProbes.html) or Reflection Probe systems are used. |
| __Cast Shadows__|  |
| &nbsp;&nbsp;&nbsp;&nbsp;On | The Mesh will cast a shadow when a shadow-casting Light shines on it |
| &nbsp;&nbsp;&nbsp;&nbsp;Off | The Mesh will not cast shadows |
| &nbsp;&nbsp;&nbsp;&nbsp;Two Sided | Two sided shadows are cast from either side of the Mesh. Two sided shadows are not supported by Enlighten or Progressive Lightmapper.|
| &nbsp;&nbsp;&nbsp;&nbsp;Shadows Only | Shadows from the Mesh will be visible, but not the Mesh  itself |
| __Receive Shadows__| Enable this check box to make the Mesh display any shadows that are cast upon it. Review Shadows is only supported when using Progressive Lightmapper|
| __Motion Vectors__| If enabled, the line has motion vectors rendered into the Camera motion vector Texture. See [Renderer.motionVectorGenerationMode](ScriptRef:Renderer-motionVectorGenerationMode.html) in the Scripting API reference documentation to learn more. |
| __Lightmap Static__| Enable this check box to indicate to Unity that the object’s location is fixed and it will participate in Global Illumination computations. If an object is not marked as Lightmap Static then it can still be lit using [Light Probes](LightProbes). |
| __Materials__| A list of Materials to render the model with. |
| __Dynamic Occluded__| Enable this check box to indicate to Unity that occlusion culling should be performed for this object even if it is not marked as static.


Tick the lightmap static checkbox to display MeshRenderer Lightmap information in the Inspector(see also the __static__ checkbox of the game object).

![](../uploads/Main/class-MeshRenderer-1.png)

![](../uploads/Main/class-MeshRenderer-2.png)

## UV Charting Control

| **Property:** | **Function:** |
|:---|:---| 
| __Optimize Realtime Uvs__| Specifies whether the authored Mesh UVs are optimized for Realtime Global Illumination or not. When enabled, the authored UVs are merged, scaled and packed for optimisation purposes. <br/>When disabled, the authored UVs will be scaled and packed, but not merged. <br/>Note that the optimization will sometimes make misjudgements about discontinuities in the original UV mapping. For example, an intentionally sharp edge may be misinterpreted as a continuous surface. |
| __Max Distance__| Specifies the maximum worldspace distance to be used for UV chart simplification. If charts are within this distance they will be simplified. |
| __Max Angle__| Specifies the maximum angle in degrees between faces sharing a UV edge. If the angle between the faces is below this value, the UV charts will be simplified.  |
| __Ignore normal__| Check this box to prevent the UV charts from being split during the precompute process for Realtime Global Illumination lighting. |
| __Min chart size__| Specifies the minimum texel size used for a UV chart. If stitching is required a value of 4 will create a chart of 4x4 texels to store lighting and directionality. If stitching is not required, a value of 2 will reduce the texel density and provide better lighting build times and game performance.  |

## Lightmap settings

| **Property:** | **Function:** |
|:---|:---| 
| __Scale in Lightmap__| This value specifies the relative size of the object's UVs within a lightmap. A value of 0 will result in the object not being lightmapped, but still contribute to lighting other objects in the scene. A value greater than 1.0 increases the number of pixels (ie, the lightmap resolution) used for this object while a value less than 1.0 decreases it. You can use this property to optimise lightmaps so that important and detailed areas are more accurately lit. For example: an isolated building with flat, dark walls will use a low lightmap scale (less than 1.0) while a collection of colourful motorcycles displayed close together warrant a high scale value.
| __Prioritize illumination__| Check this box to tell Unity to always include this object in lighting calculations. Useful for objects that are strongly emissive to make sure that other objects will be illuminated by this object. |
| __Lightmap Parameters__| Allows you to choose or create a set of [Lightmap Parameters](LightmapParameters) for the this object. |

##Details

Meshes imported from 3D packages can use multiple [Materials](Materials). All the Materials used by a Mesh Renderer are held in the __Materials__ list. Each sub-Mesh uses one Material from the Materials list. If there are more Materials assigned to the Mesh Renderer than there are sub-Meshes in the Mesh, the first sub-Mesh is rendered with each of the remaining Materials, one on top of the next. This allows you to set up multi-pass rendering on that sub-Mesh - but note that this can impact the performance at run time. Also note that fully opaque Materials, simply overwrite the previous layers, causing a decrease in performance with no advantage.

A Mesh can receive light from the [Light Probe](LightProbes) system and reflections from the [Reflection Probe](class-ReflectionProbe) system depending on the settings of the __Use Light Probes__ and __Use Reflection Probes__ options. For both types of probe, a single point is used as the Mesh's notional position probe interpolation. By default, this is the centre of the Mesh's bounding box, but you can change this by dragging a [Transform](class-Transform) to the __Anchor Override__ property (the Anchor Override affects both types of probe). 

It may be useful to set the anchor in cases where a GameObject contains two adjoining Meshes; since each Mesh has a separate bounding box, the two are lit discontinuously at the join by default. However, if you set both Meshes to use the same anchor point, then they are consistently lit. By default, a probe-lit Renderer receives lighting from a single Light Probe that is interpolated from the surrounding Light Probes in the Scene. Because of this, GameObjects have constant ambient lighting across the surface. It has a rotational gradient because it is using spherical harmonics, but it lacks a spatial gradient. This is more noticeable on larger objects or Particle Systems. The lighting across the GameObject matches the lighting at the anchor point, and if the GameObject straddles a lighting gradient, parts of the GameObject look incorrect. 

To alleviate this behavior, set the __Light Probes__ property to __Use Proxy Volume__, with an additional [Light Probe Proxy Volume](class-LightProbeProxyVolume) component. This generates a 3D grid of interpolated Light Probes inside a bounding volume where the resolution of the grid can be user-specified. The spherical harmonics coefficients of the interpolated Light Probes are updated into 3D Textures, which are sampled at render time to compute the contribution to the diffuse ambient lighting. This adds a spatial gradient to probe-lit GameObjects.

---

* <span class="page-edit"> 2017-06-08  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Updated supported lighting backends for Two Sided shadows and Recieve shadows.</span>

* <span class="page-history">Mesh Renderer UI updated in 5.6</span>