# Using Depth Textures


It is possible to create [Render Textures](class-RenderTexture) where each pixel contains a high-precision [Depth](ScriptRef:RenderTextureFormat.Depth.html) value. This is mostly used when some effects need the Scene's Depth to be available (for example, soft particles, screen space ambient occlusion and translucency would all need the Scene's Depth). [Image Effects](PostProcessingWritingEffects) often use Depth Textures too. 

Pixel values in the Depth Texture range between 0 and 1, with a non-linear distribution. Precision is usually 32 or 16 bits, depending on configuration and platform used. When reading from the Depth Texture, a high precision value in a range between 0 and 1 is returned. If you need to get distance from the Camera, or an otherwise linear 0-1 value, compute that manually using helper macros (see below).

Depth Textures are supported on most modern hardware and graphics APIs. Special requirements are listed below:

* Direct3D 11+ (Windows), OpenGL 3+ (Mac/Linux), OpenGL ES 3.0+ (Android/iOS), Metal (iOS) and consoles like PS4/Xbox One all support depth textures.
* OpenGL ES 2.0 (iOS/Android) requires [GL_OES_depth_texture](http://www.khronos.org/registry/gles/extensions/OES/OES_depth_texture.txt) extension to be present.
* WebGL requires [WEBGL_depth_texture](https://www.khronos.org/registry/webgl/extensions/WEBGL_depth_texture) extension.



## Depth Texture Shader helper macros


Most of the time, Depth Texture are used to render Depth from the Camera. The [UnityCG.cginc include file](SL-BuiltinIncludes) contains some macros to deal with the above complexity in this case:

* __UNITY_TRANSFER_DEPTH(o)__: computes eye space depth of the vertex and outputs it in __o__ (which must be a float2). Use it in a vertex program when rendering into a depth texture. On platforms with native depth textures this macro does nothing at all, because Z buffer value is rendered implicitly.
* __UNITY_OUTPUT_DEPTH(i)__: returns eye space depth from __i__ (which must be a float2). Use it in a fragment program when rendering into a depth texture. On platforms with native depth textures this macro always returns zero, because Z buffer value is rendered implicitly.
* __COMPUTE_EYEDEPTH(i)__: computes eye space depth of the vertex and outputs it in __o__. Use it in a vertex program when __not__ rendering into a depth texture.
* __DECODE_EYEDEPTH(i)/LinearEyeDepth(i)__: given high precision value from depth texture __i__, returns corresponding eye space depth.
* __Linear01Depth(i)__: given high precision value from depth texture __i__, returns corresponding linear depth in range between 0 and 1.

__Note:__ On DX11/12, PS4, XboxOne and Metal, the Z buffer range is 1-0 and UNITY_REVERSED_Z is defined. On other platforms, the range is 0-1.

For example, this shader would render depth of its GameObjects:

````
Shader "Render Depth" {
	SubShader {
	    Tags { "RenderType"="Opaque" }
	    Pass {
			CGPROGRAM

			#pragma vertex vert
			#pragma fragment frag
			#include "UnityCG.cginc"

			struct v2f {
			    float4 pos : SV_POSITION;
			    float2 depth : TEXCOORD0;
			};

			v2f vert (appdata_base v) {
			    v2f o;
			    o.pos = UnityObjectToClipPos(v.vertex);
			    UNITY_TRANSFER_DEPTH(o.depth);
			    return o;
			}

			half4 frag(v2f i) : SV_Target {
			    UNITY_OUTPUT_DEPTH(i.depth);
			}
			ENDCG
	    }
	}
}
````

## See also

* [Camera Depth Textures](SL-CameraDepthTexture)
* [Writing Image Effects](PostProcessingWritingEffects)