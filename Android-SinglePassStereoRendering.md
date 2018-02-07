#Single-Pass Stereo Rendering for Android

Single-pass stereo rendering is currently supported on Gear VR and Daydream devices. To enable this feature we use the [GL_OVR_multiview2](https://www.khronos.org/registry/OpenGL/extensions/OVR/OVR_multiview2.txt) and [GL_OVR_multiview_multisampled_render_to_texture](https://www.khronos.org/registry/OpenGL/extensions/OVR/OVR_multiview_multisampled_render_to_texture.txt) OpenGL|ES extensions*. These extensions require the use of a texture 2D array with 2 slices (one slice per eye). This differs from our PC/PS4 implementation where we just use a double wide 2D texture. Therefore different shader changes are required.

## Shader script requirements

You may need to include the additional code listed below to use Single-Pass Stereo Rendering with your custom shaders. This doesn’t apply to surface shaders or fixed function pipeline shaders which Unity automatically converts, except surface shaders that have custom vertex processing.

Note that these shader script changes are compatible with Multi-Pass stereo rendering, so there will be no side effects in that mode.

First, if you’d like to use `unity_StereoEyeIndex` in shader stages after the vertex shader you must declare `UNITY_VERTEX_OUTPUT_STEREO` in any shader stage output structs that you have. Here’s an example:

```
struct v2f {
    float2 uv : TEXCOOR0;
    float4 vertex : SV_POSITION;
    UNITY_VERTEX_OUTPUT_STEREO
};
```

Next, you must use `UNITY_INITIALIZE_VERTEX_OUTPUT_STEREO()` in the vertex shader function to initialize the output data:

```
v2f vert (appdata v)
{
	v2f o;
	UNITY_INITIALIZE_VERTEX_OUTPUT_STEREO(o);
    o.vertex = UnityObjectToClipPos(v.vertex);
    o.uv = TRANSFORM_TEX(v.uv, _MainTex);
    return o;
}
```

To initialize `unity_StereoEyeIndex` in subsequent stages you need to add `UNITY_SETUP_STEREO_EYE_INDEX_POST_VERTEX()` at the beginning like so:

```
fixed4 frag (v2f i) : SV_Target
{
    UNITY_SETUP_STEREO_EYE_INDEX_POST_VERTEX(i);
	// sample the texture
	fixed4 col = tex2D(_MainTex, i.uv);
	// apply fog
	UNITY_APPLY_FOG(i.fogCoord, col);
	return col;
}

```

If you are using other shader stages you should also use the `UNITY_TRANSFER_VERTEX_OUTPUT_STEREO()`macro to transfer the eye index to the subsequent stages.

Finally, we recommend that you use `UnityObjectToClipPos(IN.vertex)` instead of mul`(UNITY_MATRIX_MVP, IN.vertex)` to calculate the final position of the object.

#Post-Processing Shaders

Post-Processing shaders will need to be updated to deal with the eye textures being a texture 2D array. To help out with this we’ve created the following macro: `UNITY_DECLARE_SCREENSPACE_TEXTURE()`. This macro should be used to wrap all textures, so that the texture will work in both multi-pass and single-pass modes. 

When sampling the texture the following macro should be used:

`UNITY_SAMPLE_SCREENSPACE_TEXTURE()`

This macro requires that `UNITY_SETUP_STEREO_EYE_INDEX_POST_VERTEX()` has already been called beforehand when in single-pass mode. We’ve also created similar macros for depth textures and screen space shadow maps. You can see the full list at the bottom of HLSLSupport.cginc.

See the [Vertex and fragment shader examples](SL-VertexFragmentShaderExamples) page for more information on shader code.

__* These OpenGL|ES extensions are relatively new, so unfortunately there may be graphics related issues due to the drivers on these phones.__

---

* <span class="page-history">New feature in 5.5</span>

*  <span class="page-edit">2017-06-20  <!-- include IncludeTextNewPageSomeEdit --></span>
