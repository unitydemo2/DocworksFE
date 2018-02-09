#ShaderLab: Stencil

The stencil buffer can be used as a general purpose per pixel mask for saving or discarding pixels.

The stencil buffer is usually an 8 bit integer per pixel. The value can be written to, increment or decremented. Subsequent draw calls can test against the value, to decide if a pixel should be discarded before running the pixel shader.


##Syntax

###Ref
````
	Ref referenceValue
````
The value to be compared against (if Comp is anything else than _always_) and/or the value to be written to the buffer (if either Pass, Fail or ZFail is set to replace). 0-255 integer.

###ReadMask
````
	ReadMask readMask
````
An 8 bit mask as an 0-255 integer, used when comparing the reference value with the contents of the buffer (_referenceValue_ & _readMask_) _comparisonFunction_ (_stencilBufferValue_ & _readMask_). Default: _255_.

###WriteMask
````
	WriteMask writeMask
````
An 8 bit mask as an 0-255 integer, used when writing to the buffer. Note that, like other write masks, it specifies which bits of stencil buffer will be affected by write (i.e. WriteMask 0 means that no bits are affected and not that 0 will be written).  Default: _255_.

###Comp
````
	Comp comparisonFunction
````
The function used to compare the reference value to the current contents of the buffer. Default: _always_.

###Pass
````
	Pass stencilOperation
````
What to do with the contents of the buffer if the stencil test (and the depth test) passes. Default: _keep_.

###Fail
````
	Fail stencilOperation
````
What to do with the contents of the buffer if the stencil test fails. Default: _keep_.

###ZFail
````
	ZFail stencilOperation
````
What to do with the contents of the buffer if the stencil test passes, but the depth test fails. Default: _keep_.


Comp, Pass, Fail and ZFail will be applied to the front-facing geometry, unless _Cull Front_ is specified, in which case it's back-facing geometry. You can also explicitly specify the two-sided stencil state by defining CompFront, PassFront, FailFront, ZFailFront (for front-facing geometry), and CompBack, PassBack, FailBack, ZFailBack (for back-facing geometry).

###Comparison Function
Comparison function is one of the following:

| | |
|:---|:---|
|**Greater** |Only render pixels whose reference value is greater than the value in the buffer.|
|**GEqual** |Only render pixels whose reference value is greater than or equal to the value in the buffer.|
|**Less** |Only render pixels whose reference value is less than the value in the buffer.|
|**LEqual** |Only render pixels whose reference value is less than or equal to the value in the buffer.|
|**Equal** |Only render pixels whose reference value equals the value in the buffer.|
|**NotEqual** |Only render pixels whose reference value differs from the value in the buffer.|
|**Always** |Make the stencil test always pass.|
|**Never** |Make the stencil test always fail.|

###Stencil Operation
Stencil operation is one of the following:

| | |
|:---|:---|
|**Keep** |Keep the current contents of the buffer.|
|**Zero** |Write 0 into the buffer.|
|**Replace** |Write the reference value into the buffer.|
|**IncrSat** |Increment the current value in the buffer. If the value is 255 already, it stays at 255.|
|**DecrSat** |Decrement the current value in the buffer. If the value is 0 already, it stays at 0.|
|**Invert** |Negate all the bits.|
|**IncrWrap** |Increment the current value in the buffer. If the value is 255 already, it becomes 0.|
|**DecrWrap** |Decrement the current value in the buffer. If the value is 0 already, it becomes 255.|



##Deferred rendering path

Stencil functionality for objects rendered in the deferred rendering path is somewhat limited, as during the base pass and lighting pass the stencil buffer is used for other purposes. During those two stages stencil state defined in the shader will be ignored and only taken into account during the final pass. Because of that it's not possible to mask out these objects based on a stencil test, but they can still modify the buffer contents, to be used by objects rendered later in the frame. Objects rendered in the forward rendering path following the deferred path (e.g. transparent objects or objects without a surface shader) will set their stencil state normally again.

The deferred rendering path uses the three highest bits of the stencil buffer, plus up to four more highest bits - depending on how many light mask layers are used in the scene. It is possible to operate within the range of the "clean" bits using the stencil read and write masks, or you can force the camera to clean the stencil buffer after the lighting pass using Camera.clearStencilAfterLightingPass.

###Example


The first example shader will write the value '2' wherever the depth test passes. The stencil test is set to always pass.



````
Shader "Red" {
	SubShader {
		Tags { "RenderType"="Opaque" "Queue"="Geometry"}
		Pass {
			Stencil {
				Ref 2
				Comp always
				Pass replace
			}
		
			CGPROGRAM
			#pragma vertex vert
			#pragma fragment frag
			struct appdata {
				float4 vertex : POSITION;
			};
			struct v2f {
				float4 pos : SV_POSITION;
			};
			v2f vert(appdata v) {
				v2f o;
				o.pos = UnityObjectToClipPos(v.vertex);
				return o;
			}
			half4 frag(v2f i) : SV_Target {
				return half4(1,0,0,1);
			}
			ENDCG
		}
	} 
}
````

The second shader will pass only for the pixels which the first (red) shader passed, because it is checking for equality with the value '2'. It will also decrement the value in the buffer wherever it fails the Z test.



````
Shader "Green" {
	SubShader {
		Tags { "RenderType"="Opaque" "Queue"="Geometry+1"}
		Pass {
			Stencil {
				Ref 2
				Comp equal
				Pass keep 
				ZFail decrWrap
			}
		
			CGPROGRAM
			#pragma vertex vert
			#pragma fragment frag
			struct appdata {
				float4 vertex : POSITION;
			};
			struct v2f {
				float4 pos : SV_POSITION;
			};
			v2f vert(appdata v) {
				v2f o;
				o.pos = UnityObjectToClipPos(v.vertex);
				return o;
			}
			half4 frag(v2f i) : SV_Target {
				return half4(0,1,0,1);
			}
			ENDCG
		}
	} 
}
````

The third shader will only pass wherever the stencil value is '1', so only pixels at the intersection of both red and green spheres - that is, where the stencil is set to '2' by the red shader and decremented to '1' by the green shader.



````
Shader "Blue" {
	SubShader {
		Tags { "RenderType"="Opaque" "Queue"="Geometry+2"}
		Pass {
			Stencil {
				Ref 1
				Comp equal
			}
		
			CGPROGRAM
			#include "UnityCG.cginc"
			#pragma vertex vert
			#pragma fragment frag
			struct appdata {
				float4 vertex : POSITION;
			};
			struct v2f {
				float4 pos : SV_POSITION;
			};
			v2f vert(appdata v) {
				v2f o;
				o.pos = UnityObjectToClipPos(v.vertex);
				return o;
			}
			half4 frag(v2f i) : SV_Target {
				return half4(0,0,1,1);
			}
			ENDCG
		}
	}
}
````

The result:

![](../uploads/Main/StencilExample.png) 


Another example of a more directed effect. The sphere is first rendered with this shader to mark-up the proper regions in the stencil buffer:



````
Shader "HolePrepare" {
	SubShader {
		Tags { "RenderType"="Opaque" "Queue"="Geometry+1"}
		ColorMask 0
		ZWrite off
		Stencil {
			Ref 1
			Comp always
			Pass replace
		}

		CGINCLUDE
			struct appdata {
				float4 vertex : POSITION;
			};
			struct v2f {
				float4 pos : SV_POSITION;
			};
			v2f vert(appdata v) {
				v2f o;
				o.pos = UnityObjectToClipPos(v.vertex);
				return o;
			}
			half4 frag(v2f i) : SV_Target {
				return half4(1,1,0,1);
			}
		ENDCG

		Pass {
			Cull Front
			ZTest Less
		
			CGPROGRAM
			#pragma vertex vert
			#pragma fragment frag
			ENDCG
		}
		Pass {
			Cull Back
			ZTest Greater
		
			CGPROGRAM
			#pragma vertex vert
			#pragma fragment frag
			ENDCG
		}
	} 
}
````

And then rendered once more as a fairly standard surface shader, with the exception of front face culling, disabled depth test and stencil test discarding previously marked pixels:



````
Shader "Hole" {
	Properties {
		_Color ("Main Color", Color) = (1,1,1,0)
	}
	SubShader {
		Tags { "RenderType"="Opaque" "Queue"="Geometry+2"}

		ColorMask RGB
		Cull Front
		ZTest Always
		Stencil {
			Ref 1
			Comp notequal 
		}

		CGPROGRAM
		#pragma surface surf Lambert
		float4 _Color;
		struct Input {
			float4 color : COLOR;
		};
		void surf (Input IN, inout SurfaceOutput o) {
			o.Albedo = _Color.rgb;
			o.Normal = half3(0,0,-1);
			o.Alpha = 1;
		}
		ENDCG
	} 
}
````

The result:

![](../uploads/Main/StencilExample2.png) 
