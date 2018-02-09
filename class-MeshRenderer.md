# Mesh Renderer

|**5.6 DRAFT ADDITION TO DOCUMENTATION** |
|:---|
|This feature has additional or changed functionality in Unity 5.6. The link below is first draft document of that addition or change. As such, the information in this document may be subject to change before final release.<br/><br/>See first draft [Light Modes](https://docs.google.com/document/d/116JvLXljfbdfllOLlyzVvWmNWpbUwcYKV16blVHuS2E/edit) documentation.|

The __Mesh Renderer__ takes the geometry from the [Mesh Filter](class-MeshFilter) and renders it at the position defined by the object's [Transform](class-Transform) component.

![](../uploads/Main/InspectorMeshRend.png) 

##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Cast Shadows__ |If enabled, the Mesh creates shadows when a shadow-casting [Light](class-Light) shines on it. The options are __On__ and __Off__ to enable/disable shadows, __Two Sided__ to allow shadows to be cast from either side of the mesh (ie, backface culling is not taken into account) and __Shadows Only__ (that is, the shadows should be visible, but not the Mesh itself). |
|__Receive Shadows__ |If enabled, the Mesh displays any shadows being cast upon it. |
|__Motion Vectors__ |If enabled, the line has motion vectors rendered into the Camera motion vector Texture. See [Renderer.motionVectors](ScriptRef:Renderer-motionVectors.html) in the Scripting API reference documentation to learn more. |
|__Materials__ |A list of Materials to render the model with. |
|__Light Probes__ |Probe-based lighting interpolation mode.  |
|__Reflection Probes__ |If enabled and reflection probes are present in the Scene, a reflection Texture is picked for this GameObject and set as a built-in Shader uniform variable. |
|__Anchor Override__ |A Transform used to determine the interpolation position when the Light Probe or Reflection Probe systems are used. |

##Details

Meshes imported from 3D packages can use multiple [Materials](Materials). All the Materials used by a Mesh Renderer are held in the __Materials__ list. Each sub-Mesh uses one Material from the Materials list. If there are more Materials assigned to the Mesh Renderer than there are sub-Meshes in the Mesh, the first sub-Mesh is rendered with each of the remaining Materials, one on top of the next. This allows you to set up multi-pass rendering on that sub-Mesh - but note that this can impact the performance at run time. Also note that fully opaque Materials, simply overwrite the previous layers, causing a decrease in performance with no advantage.

A Mesh can receive light from the [Light Probe](LightProbes) system and reflections from the [Reflection Probe](class-ReflectionProbe) system depending on the settings of the __Use Light Probes__ and __Use Reflection Probes__ options. For both types of probe, a single point is used as the Mesh's notional position probe interpolation. By default, this is the centre of the Mesh's bounding box, but you can change this by dragging a [Transform](class-Transform) to the __Anchor Override__ property (the Anchor Override affects both types of probe). 

It may be useful to set the anchor in cases where a GameObject contains two adjoining Meshes; since each Mesh has a separate bounding box, the two are lit discontinuously at the join by default. However, if you set both Meshes to use the same anchor point, then they are consistently lit. By default, a probe-lit Renderer receives lighting from a single Light Probe that is interpolated from the surrounding Light Probes in the Scene. Because of this, GameObjects have constant ambient lighting across the surface. It has a rotational gradient because it is using spherical harmonics, but it lacks a spatial gradient. This is more noticeable on larger objects or Particle Systems. The lighting across the GameObject matches the lighting at the anchor point, and if the GameObject straddles a lighting gradient, parts of the GameObject look incorrect. 

To alleviate this behavior, set the __Light Probes__ property to __Use Proxy Volume__, with an additional [Light Probe Proxy Volume](class-LightProbeProxyVolume) component. This generates a 3D grid of interpolated Light Probes inside a bounding volume where the resolution of the grid can be user-specified. The spherical harmonics coefficients of the interpolated Light Probes are updated into 3D Textures, which are sampled at render time to compute the contribution to the diffuse ambient lighting. This adds a spatial gradient to probe-lit GameObjects.