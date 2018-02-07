#Single-Pass Stereo Rendering for HoloLens

There are two stereo rendering methods for Windows Holographic devices (HoloLens); multi-pass and single-pass instanced. 

##Multi-pass

Multi-pass rendering runs 2 complete render passes (one for each eye). This generates almost double the CPU workload compared to the single-pass instanced rendering method. However this method is the most backwards compatible and doesn’t require any shader changes.

##Single-pass Instanced

Instanced rendering performs a single render pass where each draw call is replaced with an instanced draw call. This heavily decreases CPU utilization. Additionally this slightly decreases GPU utilization due to the cache coherency between the two draw calls. In turn your app’s power consumption will be much lower.

To enable this feature, open __PlayerSettings __(menu: __Edit __> __Project Settings __> __Player__). In __PlayerSettings__, navigate to __Other Settings__, check the __Virtual Reality Supported__ checkbox, then select __Single Pass Instanced (Fastest)__ from the __Stereo Rendering Method__ dropdown.

![](../uploads/Main/SinglePassHoloLens1.png)

Unity defaults to the slower __Multi pass (Slow)__ setting as you may have custom shaders that do not have the required code in your scripts to support this feature.

##Shader script requirements

Any non built-in shaders will need to be updated to work with instancing. Please read this documentation to see how this is done: [GPU Instancing](GPUInstancing). Furthermore, you’ll need to make two additional changes in the last shader stage used before the fragment shader (Vertex/Hull/Domain/Geometry). First, you will have to add `UNITY_VERTEX_OUTPUT_STEREO` to the output struct. Second, you will need to add `UNITY_INITIALIZE_VERTEX_OUTPUT_STEREO()` in the main function for that stage after `UNITY_SETUP_INSTANCE_ID()` has been called.

__Post-Processing Shaders__

You will need to add the `UNITY_DECLARE_SCREENSPACE_TEXTURE(tex)` macro around the input texture declarations, so that 2D texture arrays will be properly declared. Next, you must add a call to `UNITY_SETUP_INSTANCE_ID()` at the beginning of the fragment shader. Finally, you will need to use the `UNITY_SAMPLE_SCREENSPACE_TEXTURE()` macro when sampling those textures. See [HLSLSupport.cginc](SL-BuiltinIncludes) for more information on other similar macros depth textures and screen space shadow maps.

Here’s a simple example that applies all of the previously mentioned changes to the template image effect:

```
struct appdata
{
    float4 vertex : POSITION;
    float2 uv : TEXCOORD0;
    UNITY_INSTANCE_ID
};
struct v2f
{
    float2 uv : TEXCOORD0;
    float4 vertex : SV_POSITION;
    UNITY_INSTANCE_ID
    UNITY_VERTEX_OUTPUT_STEREO
};
v2f vert (appdata v)
{
    v2f o;
    UNITY_SETUP_INSTANCE_ID(v);
    UNITY_TRANSFER_INSTANCE_ID(v, o);
    UNITY_INITIALIZE_VERTEX_OUTPUT_STEREO(o);
    o.vertex = UnityObjectToClipPos(v.vertex);
    o.uv = v.uv;
    return o;
}

UNITY_DECLARE_SCREENSPACE_TEXTURE(_MainTex);

fixed4 frag (v2f i) : SV_Target
{
    UNITY_SETUP_INSTANCE_ID(i);
    fixed4 col = UNITY_SAMPLE_SCREENSPACE_TEXTURE(_MainTex, i.uv);
    // just invert the colors
    col = 1 - col;
    return col;
}
```

#DrawProceduralIndirect

`Graphics.DrawProceduralIndirect()` and `CommandBuffer.DrawProceduralIndirect()` get all of their arguments from a compute buffer, so we can’t easily increase the instance count. Therefore you will have to manually double the instance count contained in your compute buffers.

See the [Vertex and fragment shader examples](SL-VertexFragmentShaderExamples) page for more information on shader code.

---

* <span class="page-edit">2017-09-01  <!-- include IncludeTextAmendPageSomeEdit --></span>
* <span class="page-history">New feature in 5.5</span>
* <span class="page-history">Fixed example code for single pass stereo rendering for HoloLens</span>



