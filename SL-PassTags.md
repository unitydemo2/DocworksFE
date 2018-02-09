#ShaderLab: Pass Tags

Passes use tags to tell how and when they expect to be rendered to the rendering engine.


##Syntax

````
	Tags { "TagName1" = "Value1" "TagName2" = "Value2" }
````
Specifies **TagName1** to have **Value1**, **TagName2** to have **Value2**. You can have as many tags as you like.


##Details


Tags are basically key-value pairs. Inside a [Pass](SL-Pass) tags are used to control which role this pass has in the lighting pipeline (ambient, vertex lit, pixel lit etc.) and some other options. Note that the following tags recognized by Unity _must_ be inside Pass section and not inside SubShader!

###LightMode tag

**LightMode** tag defines Pass' role in the lighting pipeline. See [render pipeline](SL-RenderPipeline) for details. These tags are rarely used manually; most often shaders that need to interact with lighting are written as [Surface Shaders](SL-SurfaceShaders) and then all those details are taken care of.

Possible values for LightMode tag are:

* **Always**: Always rendered; no lighting is applied.
* **ForwardBase**: Used in [Forward rendering](RenderTech-ForwardRendering), ambient, main directional light, vertex/SH lights and lightmaps are applied.
* **ForwardAdd**: Used in [Forward rendering](RenderTech-ForwardRendering); additive per-pixel lights are applied, one pass per light.
* **Deferred**: Used in [Deferred Shading](RenderTech-DeferredShading); renders g-buffer.
* **ShadowCaster**: Renders object depth into the shadowmap or a depth texture.
* **MotionVectors**: Used to calculate per-object motion vectors.
* **PrepassBase**: Used in [legacy Deferred Lighting](RenderTech-DeferredLighting), renders normals and specular exponent.
* **PrepassFinal**: Used in [legacy Deferred Lighting](RenderTech-DeferredLighting), renders final color by combining textures, lighting and emission.
* **Vertex**: Used in [legacy Vertex Lit rendering](RenderTech-VertexLit) when object is not lightmapped; all vertex lights are applied.
* **VertexLMRGBM**: Used in [legacy Vertex Lit rendering](RenderTech-VertexLit) when object is lightmapped; on platforms where lightmap is RGBM encoded (PC & console).
* **VertexLM**: Used in [legacy Vertex Lit rendering](RenderTech-VertexLit) when object is lightmapped; on platforms where lightmap is double-LDR encoded (mobile platforms).


### PassFlags tag

A pass can indicate flags that change how [rendering pipeline](SL-RenderPipeline) passes data to it. This is done by using **PassFlags** tag, with a value that is space-separated flag names. Currently the flags supported are:

* **OnlyDirectional**: When used in ForwardBase pass type, this flag makes it so that only the main directional light and ambient/lightprobe data is passed into the shader. This means that data of non-important lights is *not* passed into vertex-light or spherical harmonics shader variables. See [Forward rendering](RenderTech-ForwardRendering) for details.


###RequireOptions tag

A pass can indicate that it should only be rendered when some external conditions are met. This is done by using **RequireOptions** tag, whose value is a string of space separated options. Currently the options supported by Unity are:

* **SoftVegetation**: Render this pass only if Soft Vegetation is on in [Quality Settings](class-QualitySettings).


##See Also

SubShaders can be given Tags as well, see [SubShader Tags](SL-SubShaderTags).
