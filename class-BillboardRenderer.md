#Billboard Renderer

The Billboard Renderer renders [BillboardAssets](class-BillboardAsset), either from a premade Asset (exported from SpeedTree) or from a custom-created file (created using a script at runtime or from a custom editor, for example). For more information about creating Billboard Assets, see the [BillboardAssets](class-BillboardAsset) manual page and the [BillboardAsset](ScriptRef:BillboardAsset.html) API reference.

Billboards are a level-of-detail (LOD) method of drawing complicated 3D Meshes in a simpler manner when they are distant in a Scene. Because the Mesh is distant, its size on screen and the low likelihood of it being a focal point in the Camera view means there is often less requirement to draw it in full detail.


![](../uploads/Main/BillboardRenderer.png)


|**Property:** |**Function:** |
|:---|:---|
| __Cast Shadows__| If enabled, the billboard creates shadows when a shadow-casting Light shines on it.|
|&nbsp;&nbsp;&nbsp;&nbsp; _On_ | Enable shadows. |
|&nbsp;&nbsp;&nbsp;&nbsp; _Off_ | Disable shadows. |
|&nbsp;&nbsp;&nbsp;&nbsp; _Two Sided_ | Allow shadows to be cast from either side of the billboard (that is, backface culling is not taken into account). |
|&nbsp;&nbsp;&nbsp;&nbsp; _Shadows Only_ | Show shadows, but not the billboard itself. |
| __Receive Shadows__ | Check the box to enable shadows to be cast on the billboard. |
| __Motion Vectors__ | Check the box to enable rendering of the billboard's motion vectors into the Camera Motion Vector Texture. See [Renderer.motionVectors](ScriptRef:Renderer-motionVectors.html) in the Scripting API for more information. |
| __Billboard__ | If you have a pre-made Billboard Asset, place it here to assign it to this Billboard Renderer. |
| __Light Probes__ | If enabled, and if baked [Light Probes](LightProbes) are present in the Scene, the Billboard Renderer uses an interpolated Light Probe for lighting. |
|&nbsp;&nbsp;&nbsp;&nbsp; _Off_ | Disable Light Probes. |
|&nbsp;&nbsp;&nbsp;&nbsp; _Blend Probes_ | The lighting applied to the billboard is interpreted from one interpolated Light Probe. |
|&nbsp;&nbsp;&nbsp;&nbsp; _Use Proxy Volume_ | The lighting applied to the Billboard Renderer is interpreted from a 3D grid of interpolated Light Probes. |
| __Reflection Probes__ | If enabled, and if [Reflection Probes](ReflectionProbes) are present in the Scene, a reflection Texture is picked for this GameObject and set as a built-in Shader uniform variable. |
|&nbsp;&nbsp;&nbsp;&nbsp; _Off_ | Disable Reflection Probes. |
|&nbsp;&nbsp;&nbsp;&nbsp; _Blend Probes_ | The reflections applied to the billboard are interpreted from adjacent Reflection Probes, and do not take the the skybox into account. This is generally used for GameObjects that are "indoors" or in covered parts of the Scene (such as caves and tunnels), because the sky is not visible and therefore wouldn’t be reflected by the billboard. |
|&nbsp;&nbsp;&nbsp;&nbsp; _Blend Probes and Skybox_ | This works like Blend Probes, but also allows the skybox to be used in the blending. This is generally used for GameObjects in the open air, where the sky would always be visible and reflected. |
|&nbsp;&nbsp;&nbsp;&nbsp; _Simple_ | Reflection Probes are enabled, but no blending occurs between probes when there are two overlapping volumes. |