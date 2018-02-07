# Particle System vertex streams and Standard Shader support

If you are comfortable writing your own Shaders, use this addition to the [Renderer Module](ScriptRef:ParticleSystemRenderer.html) to configure your Particle Systems to pass a wider range of data into your custom Shaders.

There are a number of built-in [data streams](ScriptRef:ParticleSystemVertexStreams.html) to choose from, such as velocity, size and center position. Aside from the ability to create powerful custom Shaders, these streams allow a number of more general benefits:

* Use the [Tangent](ScriptRef:ParticleSystemVertexStream.Tangent.html) stream to support normal mapped particles.
* You can remove Color and then add the Tangent [UV2](ScriptRef:ParticleSystemVertexStream.UV2.html) and [AnimBlend](ScriptRef:ParticleSystemVertexStream.AnimBlend.html) streams to use the Standard Shader on particles.
* To easily perform linear texture blending of flipbooks, add the UV2 and AnimBlend streams, and attach the Particles/Anim Alpha Blended Shader (see example screenshot below to see how to set this up).


There are also two completely custom per-particle data streams ([ParticleSystemVertexStreams.Custom1](ScriptRef:ParticleSystemVertexStreams.Custom1.html) and [ParticleSystemVertexStreams.Custom2](ScriptRef:ParticleSystemVertexStreams.Custom2.html)), which can be populated from script. Call [SetCustomParticleData](ScriptRef:ParticleSystem.SetCustomParticleData.html) and [GetCustomParticleData](ScriptRef:ParticleSystem.GetCustomParticleData.html) with your array of data to use them. There are two ways of using this:

* To drive custom behavior in scripts by attaching your own data to particles; for example, attaching a “health” value to each particle.
* To pass this data into a Shader by adding one of the two custom streams, in the same way you would send any other stream to your Shader (see [ParticleSystemRenderer.EnableVertexStreams](ScriptRef:ParticleSystemRenderer.EnableVertexStreams.html)). To elaborate on the first example, maybe your custom health attribute could now also drive some kind of visual effect, as well as driving script-based game logic.

When adding vertex streams, Unity will provide you with some information in brackets, next to each item, to help you read the correct data in your shader:


![](../uploads/Main/PartSysVertexStreams-VertexShaders.png)

Each item in brackets corresponds to a Vertex Shader input, which you should specify in your Shader. Here is the correct input structure for this configuration.

````
			struct appdata_t {
				float4 vertex : POSITION;
				float3 normal : NORMAL;
				fixed4 color : COLOR;
				float4 texcoords : TEXCOORD0;
				float texcoordBlend : TEXCOORD1;
			};
````
Notice that both UV and UV2 are passed in different parts of TEXCOORD0, so we use a single declaration for both. To access each one in your shader, you would use the xy and zw swizzles. This allows you to pack your vertex data efficiently.

Here is an example of an animated flip-book Shader. It uses the default inputs (__Position__, __Normal__, __Color__, __UV__), but also uses two additional streams for the second UV stream (__UV2__) and the flip-book frame information (__AnimBlend__).

![](../uploads/Main/PartSysVertexStreams-Inspector.png)

````
Shader "Particles/Anim Alpha Blended" {
Properties {
	_TintColor ("Tint Color", Color) = (0.5,0.5,0.5,0.5)
	_MainTex ("Particle Texture", 2D) = "white" {}
	_InvFade ("Soft Particles Factor", Range(0.01,3.0)) = 1.0
}

Category {
	Tags { "Queue"="Transparent" "IgnoreProjector"="True" "RenderType"="Transparent" "PreviewType"="Plane" }
	Blend SrcAlpha OneMinusSrcAlpha
	ColorMask RGB
	Cull Off Lighting Off ZWrite Off

	SubShader {
		Pass {
		
			CGPROGRAM
			#pragma vertex vert
			#pragma fragment frag
			#pragma target 2.0
			#pragma multi_compile_particles
			#pragma multi_compile_fog
			
			#include "UnityCG.cginc"

			sampler2D _MainTex;
			fixed4 _TintColor;
			
			struct appdata_t {
				float4 vertex : POSITION;
				fixed4 color : COLOR;
				float4 texcoords : TEXCOORD0;
				float texcoordBlend : TEXCOORD1;
				UNITY_VERTEX_INPUT_INSTANCE_ID
			};

			struct v2f {
				float4 vertex : SV_POSITION;
				fixed4 color : COLOR;
				float2 texcoord : TEXCOORD0;
				float2 texcoord2 : TEXCOORD1;
				fixed blend : TEXCOORD2;
				UNITY_FOG_COORDS(3)
				#ifdef SOFTPARTICLES_ON
				float4 projPos : TEXCOORD4;
				#endif
				UNITY_VERTEX_OUTPUT_STEREO
			};
			
			float4 _MainTex_ST;

			v2f vert (appdata_t v)
			{
				v2f o;
				UNITY_SETUP_INSTANCE_ID(v);
				UNITY_INITIALIZE_VERTEX_OUTPUT_STEREO(o); 
				o.vertex = UnityObjectToClipPos(v.vertex);
				#ifdef SOFTPARTICLES_ON
				o.projPos = ComputeScreenPos (o.vertex);
				COMPUTE_EYEDEPTH(o.projPos.z);
				#endif
				o.color = v.color * _TintColor;
				o.texcoord = TRANSFORM_TEX(v.texcoords.xy,_MainTex);
				o.texcoord2 = TRANSFORM_TEX(v.texcoords.zw,_MainTex);
				o.blend = v.texcoordBlend;
				UNITY_TRANSFER_FOG(o,o.vertex);
				return o;
			}

			sampler2D_float _CameraDepthTexture;
			float _InvFade;
			
			fixed4 frag (v2f i) : SV_Target
			{
				#ifdef SOFTPARTICLES_ON
				float sceneZ = LinearEyeDepth (SAMPLE_DEPTH_TEXTURE_PROJ(_CameraDepthTexture, UNITY_PROJ_COORD(i.projPos)));
				float partZ = i.projPos.z;
				float fade = saturate (_InvFade * (sceneZ-partZ));
				i.color.a *= fade;
				#endif
				
				fixed4 colA = tex2D(_MainTex, i.texcoord);
				fixed4 colB = tex2D(_MainTex, i.texcoord2);
				fixed4 col = 2.0f * i.color * lerp(colA, colB, i.blend);
				UNITY_APPLY_FOG(i.fogCoord, col);
				return col;
			}
			ENDCG 
		}
	}	
}
}


````

It’s also possible to use Surface Shaders with this system, although there are some extra things to be aware of:

* The input structure to your surface function is not the same as the input structure to the vertex Shader. You need to provide your own vertex Shader input structure. See below for an example, where it is called `appdata_particles`.
* When surface Shaders are built, there is automatic handling of variables whose names begin with certain tokens. The most notable one is `uv`. To prevent the automatic handling from causing problems here, be sure to give your UV inputs different names (for example, “texcoord”).

Here is the same functionality as the first example, but in a Surface Shader:

````
Shader "Particles/Anim Alpha Blend Surface" {
    Properties {
        _Color ("Color", Color) = (1,1,1,1)
        _MainTex ("Albedo (RGB)", 2D) = "white" {}
        _Glossiness ("Smoothness", Range(0,1)) = 0.5
        _Metallic ("Metallic", Range(0,1)) = 0.0
    }
    SubShader {
        Tags {"Queue"="Transparent" "RenderType"="Transparent"}
        Blend SrcAlpha OneMinusSrcAlpha
        ZWrite off
        LOD 200
        
        CGPROGRAM
        // Physically based Standard lighting model, and enable shadows on all light types
        #pragma surface surf Standard alpha vertex:vert

        // Use shader model 3.0 target, to get nicer looking lighting
        #pragma target 3.0

        sampler2D _MainTex;

         struct appdata_particles {
            float4 vertex : POSITION;
            float3 normal : NORMAL;
            float4 color : COLOR;
            float4 texcoords : TEXCOORD0;
            float texcoordBlend : TEXCOORD1;
            };


        struct Input {
            float2 uv_MainTex;
            float2 texcoord1;
            float blend;
            float4 color;
        };


        void vert(inout appdata_particles v, out Input o) {
            UNITY_INITIALIZE_OUTPUT(Input,o);
            o.uv_MainTex = v.texcoords.xy;
            o.texcoord1 = v.texcoords.zw;
            o.blend = v.texcoordBlend;
            o.color = v.color;
          }


        half _Glossiness;
        half _Metallic;
        fixed4 _Color;


        void surf (Input IN, inout SurfaceOutputStandard o) {
            fixed4 colA = tex2D(_MainTex, IN.uv_MainTex);
            fixed4 colB = tex2D(_MainTex, IN.texcoord1);
            fixed4 c = 2.0f * IN.color * lerp(colA, colB, IN.blend) * _Color;
                 
            o.Albedo = c.rgb;
            // Metallic and smoothness come from slider variables
            o.Metallic = _Metallic;
            o.Smoothness = _Glossiness;
            o.Alpha = c.a;
        }
        ENDCG
    }
    FallBack "Diffuse"
}

````
----

* <span class="page-edit">2017-05-15  <!-- include IncludeTextAmendPageNoEdit --></span>

