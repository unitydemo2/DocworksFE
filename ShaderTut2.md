# Shaders: vertex and fragment programs


This tutorial will teach you the basics of how to write [vertex and fragment programs](SL-ShaderPrograms) in Unity shaders. For a basic introduction to ShaderLab see the [Getting Started tutorial](ShaderTut1). If you want to write shaders that interact with lighting, read about [Surface Shaders](SL-SurfaceShaders) instead.

Lets start with a small recap of the general structure of a shader:




```
Shader "MyShaderName"
{
    Properties
    {
        // material properties here
    }
    SubShader // subshader for graphics hardware A
    {
        Pass
        {
            // pass commands ...
        }
        // more passes if needed
    }
    // more subshaders if needed
    FallBack "VertexLit" // optional fallback
}

```

Here at the end we introduce a new command: __FallBack "VertexLit"__.
The [Fallback](SL-Fallback) command can be used at the end of the
shader; it tells which shader should be used if no
__SubShaders__ from the current shader
can run on user's graphics hardware. The effect is the same as
including all SubShaders from the fallback shader at the end.
For example, if you were to write a fancy normal-mapped shader,
then instead of writing a very basic non-normal-mapped subshader
for old graphics cards you can just fallback to built-in
__VertexLit__ shader.

The basic building blocks of the shader are introduced in the
[first shader tutorial](ShaderTut1) while the full documentation
of [Properties](SL-Properties), [SubShaders](SL-SubShader) and
[Passes](SL-Pass) are also available.

A quick way of building SubShaders is to use passes defined in
other shaders. The command [UsePass](SL-UsePass) does just that, so
you can reuse shader code in a neat fashion. As an example the
following command uses the pass with the name "FORWARD" from
the built-in __Specular__ shader:
__UsePass "Specular/FORWARD"__.

In order for __UsePass__ to work, a name
must be given to the pass one wishes to use. The [Name](SL-Name) command inside the pass
gives it a name: __Name "MyPassName"__.


## Vertex and fragment programs


We described a pass that used just a single texture combine instruction in the [first tutorial](ShaderTut1). Now it is time to demonstrate how we can use vertex and fragment programs in our pass.

When you use vertex and fragment programs (the so called "programmable pipeline"), most of the hardcoded functionality ("fixed function pipeline") in the graphics hardware is switched off. For example, using a vertex program turns off standard 3D transformations, lighting and texture coordinate generation completely. Similarly, using a fragment program replaces any texture combine modes that would be defined in SetTexture commands; thus SetTexture commands are not needed.

Writing vertex/fragment programs requires a thorough knowledge of 3D transformations, lighting and coordinate spaces - because you have to rewrite the fixed functionality that is built into APIs like OpenGL yourself. On the other hand, you can do much more than what's built in!


## Using Cg/HLSL in ShaderLab


Shaders in ShaderLab are usually written in [Cg](http://developer.nvidia.com/page/cg_main.html)/[HLSL](http://msdn.microsoft.com/en-us/library/bb509561%28VS.85%29.aspx) programming language. Cg and DX9-style HLSL are for all practical purposes one and the same language, so we'll be using Cg and HLSL interchangeably (see [this page](SL-ShadingLanguage) for details).

Shader code is written by embedding "Cg/HLSL snippets" in the shader text. Snippets are compiled into low-level shader assembly by the Unity editor, and the final shader that is included in your game's data files only contains this low-level assembly or bytecode, that is platform specific. When you select a shader in the __Project View__, the Inspector has a button to show compiled shader code, which might help as a debugging aid. Unity automatically compiles Cg snippets for all relevant platforms (Direct3D 9, OpenGL, Direct3D 11, OpenGL ES and so on). Note that because Cg/HLSL code is compiled by the editor, you can't create shaders from scripts at runtime.

In general, snippets are placed inside Pass blocks. They look like this:

```
Pass {
    // ... the usual pass state setup ...

    CGPROGRAM
    // compilation directives for this snippet, e.g.:
    #pragma vertex vert
    #pragma fragment frag

    // the Cg/HLSL code itself

    ENDCG
    // ... the rest of pass setup ...
}
```

The following example demonstrates a complete shader that renders object normals as colors:



```
Shader "Tutorial/Display Normals" {
    SubShader {
        Pass {

			CGPROGRAM

			#pragma vertex vert
			#pragma fragment frag
			#include "UnityCG.cginc"

			struct v2f {
				float4 pos : SV_POSITION;
				fixed3 color : COLOR0;
			};

			v2f vert (appdata_base v)
			{
				v2f o;
				o.pos = UnityObjectToClipPos(v.vertex);
				o.color = v.normal * 0.5 + 0.5;
				return o;
			}

			fixed4 frag (v2f i) : SV_Target
			{
				return fixed4 (i.color, 1);
			}
			ENDCG

        }
    }
}

```


When applied on an object it will result in an image like this:


![](../uploads/Main/ShaderTutNormalsShader.png) 

Our "Display Normals" shader does not have any properties, contains a single SubShader with a single Pass that is empty except for the Cg/HLSL code. Let's dissect the code part by part:

```
CGPROGRAM
#pragma vertex vert
#pragma fragment frag
// ...
ENDCG
```

The whole snippet is written between __CGPROGRAM__ and __ENDCG__ keywords. At the start compilation directives are given as __#pragma__ statements:

* __#pragma vertex name__ tells that the code contains a vertex program in the given function (__vert__ here).
* __#pragma fragment name__ tells that the code contains a fragment program in the given function (__frag__ here).

Following the compilation directives is just plain Cg/HLSL code. We start by including a [built-in include file](SL-BuiltinIncludes):

```
#include "UnityCG.cginc"
```

The __UnityCG.cginc__ file contains commonly used declarations and functions so that the shaders can be kept smaller (see [shader include files](SL-BuiltinIncludes) page for details). Here we'll use __appdata_base__ structure from that file. We could just define them directly in the shader and not include the file of course.

Next we define a "vertex to fragment" structure (here named __v2f__) - what information is passed from the vertex to the fragment program. We pass the position and color parameters. The color will be computed in the vertex program and just output in the fragment program.

We proceed by defining the vertex program - __vert__ function. Here we compute the position and output input normal as a color:
    o.color = v.normal * 0.5 + 0.5;

Normal components are in -1..1 range, while colors are in 0..1 range, so we scale and bias the normal in the code above. Next we define a fragment program - __frag__ function that just outputs the calculated color and 1 as the alpha component:

```
fixed4 frag (v2f i) : SV_Target
{
    return fixed4 (i.color, 1);
}
```

That's it, our shader is finished! Even this simple shader is very useful to visualize mesh normals.

Of course, this shader does not respond to lights at all, and that's where things get a bit more interesting; read about [Surface Shaders](SL-SurfaceShaders) for details.


## Using shader properties in Cg/HLSL code


When you define properties in the shader, you give them a name like __\_Color__ or __\_MainTex__. To use them in Cg/HLSL you just have to define a variable of a matching name and type. See [properties in shader programs](SL-PropertiesInPrograms) page for details.

Here is a complete shader that displays a texture modulated by a color. Of course, you could easily do the same in a texture combiner call, but the point here is just to show how to use properties in Cg:

```
Shader "Tutorial/Textured Colored" {
	Properties {
		_Color ("Main Color", Color) = (1,1,1,0.5)
		_MainTex ("Texture", 2D) = "white" { }
	}
	SubShader {
		Pass {

		CGPROGRAM
		#pragma vertex vert
		#pragma fragment frag

		#include "UnityCG.cginc"

		fixed4 _Color;
		sampler2D _MainTex;

		struct v2f {
			float4 pos : SV_POSITION;
			float2 uv : TEXCOORD0;
		};

		float4 _MainTex_ST;

		v2f vert (appdata_base v)
		{
			v2f o;
			o.pos = UnityObjectToClipPos(v.vertex);
			o.uv = TRANSFORM_TEX (v.texcoord, _MainTex);
			return o;
		}

		fixed4 frag (v2f i) : SV_Target
		{
			fixed4 texcol = tex2D (_MainTex, i.uv);
			return texcol * _Color;
		}
		ENDCG

		}
	}
}

```


The structure of this shader is the same as in the previous example. Here we define two properties, namely __\_Color__ and __\_MainTex__. Inside Cg/HLSL code we define corresponding variables:

```
fixed4 _Color;
sampler2D _MainTex;
```

See [Accessing Shader Properties in Cg/HLSL](SL-PropertiesInPrograms) for more information.

The vertex and fragment programs here don't do anything fancy; vertex program uses the __TRANSFORM_TEX__ macro from UnityCG.cginc to make sure texture scale and offset is applied correctly, and fragment program just samples the texture and multiplies by the color property.


## Summary


We have shown how custom shader programs can be written in a few easy steps. While the examples shown here are very simple, there's nothing preventing you to write arbitrarily complex shader programs! This can help you to take the full advantage of Unity and achieve optimal rendering results.

The complete ShaderLab reference manual is [here](SL-Reference), and more examples in [vertex and fragment shader examples](SL-VertexFragmentShaderExamples) page. We also have a forum for shaders at [forum.unity3d.com](http://forum.unity3d.com) so go there to get help with your shaders! Happy programming, and enjoy the power of Unity and ShaderLab.
