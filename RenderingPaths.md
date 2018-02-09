#Rendering Paths

Unity supports different *Rendering Paths*. You should choose which one you use depending on your game content and target platform / hardware. Different rendering paths have different performance characteristics that mostly affect Lights and Shadows. See [render pipeline](SL-RenderPipeline) for technical details.

The rendering path used by your project is chosen in [Graphics Settings](class-GraphicsSettings). Additionally, you can override it for each [Camera](class-Camera).

If the graphics card can't handle a selected rendering path, Unity will automatically use a lower fidelity one. For example, on a GPU that can't handle Deferred Shading, Forward Rendering will be used.


## Deferred Shading

*Deferred Shading* is the rendering path with the most lighting and shadow fidelity, and is best suited if you have many realtime lights. It requires a certain level of hardware support.

For more details see the [Deferred Shading page](RenderTech-DeferredShading).


## Forward Rendering

Forward is the traditional rendering path. It supports all the typical Unity graphics features (normal maps, per-pixel lights, shadows etc.). However under default settings, only a small number of the brightest lights are rendered in per-pixel lighting mode. The rest of the lights are calculated at object vertices or per-object.

For more details see the [Forward Rendering page](RenderTech-ForwardRendering).


## Legacy Deferred

*Legacy Deferred (light prepass)* is similar to Deferred Shading, just using a different technique with different trade-offs. It does not support the Unity 5 physically based standard shader.

For more details see the [Deferred Lighting page](RenderTech-DeferredLighting).


## Legacy Vertex Lit

*Legacy Vertex Lit* is the rendering path with the lowest lighting fidelity and no support for realtime shadows. It is a subset of Forward rendering path.

For more details see the [Vertex Lit page](RenderTech-VertexLit).

**NOTE:** *Deferred rendering is not supported when using Orthographic projection. If the camera's projection mode is set to Orthographic, these values are overridden, and the camera will always use Forward rendering.*

##Rendering Paths Comparison


| |**_Deferred_** |**_Forward_** |**Legacy Deferred** | **_Vertex Lit_** |
|:---                                            |:--- |:--- |:--- |:--- |
|**Features**                                    |     |     |     |     |
|Per-pixel lighting (normal maps, light cookies) | Yes | Yes | Yes | -   |
|Realtime shadows                                | Yes | With caveats | Yes | - |
|Reflection Probes                               | Yes | Yes | -   | -   |
|Depth&Normals Buffers                           | Yes | Additional render passes | Yes | - |
|Soft Particles                                  | Yes | -   | Yes | -   |
|Semitransparent objects                         | -   | Yes | -   | Yes |
|Anti-Aliasing                                   | -   | Yes | -   | Yes |
|Light Culling Masks                             | Limited | Yes | Limited | Yes |
|Lighting Fidelity                               | All per-pixel | Some per-pixel | All per-pixel | All per-vertex |
|**Performance**                                 |     |     |     |     |
|Cost of a per-pixel Light                       | Number of pixels it illuminates | Number of pixels * Number of objects it illuminates | Number of pixels it illuminates | - |
|Number of times objects are normally rendered   | 1                       | Number of per-pixel lights | 2 | 1 |
|Overhead for simple scenes                      | High                    | None | Medium             | None |
|**Platform Support**                            |                         |      |                    |      |
|PC (Windows/Mac)                                | Shader Model 3.0+ & MRT | All  | Shader Model 3.0+  | All  |
|Mobile (iOS/Android)                            | OpenGL ES 3.0 & MRT     | All  | OpenGL ES 2.0      | All  |
|Consoles                                        | XB1, PS4                | All  | XB1, PS4, 360 | -    |
