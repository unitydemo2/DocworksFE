# GPU instancing

## Introduction

Use GPU Instancing to draw (or render) multiple copies of the same Mesh at once, using a small number of [draw calls](DrawCallBatching). It is useful for drawing objects such as buildings, trees and grass, or other things that appear repeatedly in a Scene. 

GPU Instancing only renders identical Meshes with each draw call, but each instance can have different parameters (for example, color or scale) to add variation and reduce the appearance of repetition. 

GPU Instancing can reduce the number of draw calls used per Scene. This significantly improves the rendering performance of your project.

## Adding instancing to your Materials

To enable GPU Instancing on Materials, select your Material in the Project window, and in the Inspector, tick the __Enable Instancing__ checkbox.

![The __Enable Instancing__ checkbox as it appears in the Material Inspector window](../uploads/Main/GPUInstancing-0.png)

Unity only displays this checkbox if the Material Shader supports GPU Instancing. This includes Standard, StandardSpecular and all surface [Shaders](Shaders). See documentation on [standard Shaders](shader-StandardShader) for more information.

The screenshots below show the same Scene with multiple GameObjects; in the top image GPU Instancing is enabled, in the bottom image it is not.  Note the difference in __FPS__, __Batches __and __Saved by batching__.

![With GPU Instancing: A simple Scene that includes multiple identical GameObjects that have GPU Instancing enabled](../uploads/Main/GPUInstancing-1.png)

![No GPU Instancing: A simple Scene that includes multiple identical GameObjects that do not have GPU Instancing enabled.](../uploads/Main/GPUInstancing-2.png)

When you use GPU instancing, the following restrictions apply:

* Unity automatically picks MeshRenderer components and `Graphics.DrawMesh` calls for instancing. Note that [SkinnedMeshRenderer](https://docs.unity3d.com/ScriptReference/SkinnedMeshRenderer.html) is not supported.

* Unity only batches GameObjects that share the same Mesh and the same Material in a single GPU instancing draw call. Use a small number of Meshes and Materials for better instancing efficiency. To create variations, modify your shader scripts to add per-instance data (see next section to learn more about this).

You can also use the calls [Graphics.DrawMeshInstanced](ScriptRef:Graphics.DrawMeshInstanced.html) and [Graphics.DrawMeshInstancedIndirect](ScriptRef:Graphics.DrawMeshInstancedIndirect.html). to perform GPU Instancing from your scripts.

GPU Instancing is available on the following platforms and APIs:

* __DirectX 11__ and __DirectX 12__ on Windows

* __OpenGL Core 4.1+/ES3.0+__ on Windows, macOS, Linux, iOS and Android

* __Metal__ on macOS and iOS

* __Vulkan__ on Windows and Android

* __PlayStation 4__ and __Xbox One__

* __WebGL__ (requires WebGL 2.0 API)

## Adding per-instance data

By default, Unity only batches instances of GameObjects with different [Transforms](Transforms) in each instanced draw call. To add more variance to your instanced GameObjects, modify your Shader to add per-instance properties such as Material color. 

The example below demonstrates how to create an instanced Shader with different colour values for each instance.

```

Shader "Custom/InstancedColorSurfaceShader" {

	Properties {

		_Color ("Color", Color) = (1,1,1,1)

		_MainTex ("Albedo (RGB)", 2D) = "white" {}

		_Glossiness ("Smoothness", Range(0,1)) = 0.5

		_Metallic ("Metallic", Range(0,1)) = 0.0

	}

	SubShader {

		Tags { "RenderType"="Opaque" }

		LOD 200

		

		CGPROGRAM

		// Physically based Standard lighting model, and enable shadows on all light types

		#pragma surface surf Standard fullforwardshadows

		// Use Shader model 3.0 target

		#pragma target 3.0

		sampler2D _MainTex;

		struct Input {

			float2 uv_MainTex;

		};

		half _Glossiness;

		half _Metallic;

		__UNITY_INSTANCING_CBUFFER_START(Props)__

			__UNITY_DEFINE_INSTANCED_PROP(fixed4, _Color);__

		__UNITY_INSTANCING_CBUFFER_END__

		void surf (Input IN, inout SurfaceOutputStandard o) {

			fixed4 c = tex2D (_MainTex, IN.uv_MainTex) * __UNITY_ACCESS_INSTANCED_PROP(_Color)__;

			o.Albedo = c.rgb;

			o.Metallic = _Metallic;

			o.Smoothness = _Glossiness;

			o.Alpha = c.a;

		}

		ENDCG

	}

	FallBack "Diffuse"

}

```

When you declare `_Color` as an instanced property, Unity takes all `_Color` GameObjects that share a Mesh and Material and includes them in a single draw call.

```

MaterialPropertyBlock props = new MaterialPropertyBlock();
MeshRenderer renderer;

foreach (GameObject obj in objects)
{
   float r = Random.Range(0.0f, 1.0f);
   float g = Random.Range(0.0f, 1.0f);
   float b = Random.Range(0.0f, 1.0f);
   props.SetColor("_Color", new Color(r, g, b));
   
   renderer = obj.GetComponent<MeshRenderer>();
   renderer.SetPropertyBlock(props);
}
```

For these changes to take effect, you must enable GPU Instancing. To do this, select your Shader in the Project window, and in the Inspector, tick the __Enable Instancing__ checkbox.

![The Enable Instancing checkbox as shown in the Shader Inspector window](../uploads/Main/GPUInstancing-3.png)

## Adding instancing to vertex and fragment Shaders

The following example takes a simple unlit Shader and makes it capable of instancing with different colors:

```

Shader "SimplestInstancedShader"
{
    Properties
    {
        _Color ("Color", Color) = (1, 1, 1, 1)
    }

    SubShader
    {
        Tags { "RenderType"="Opaque" }
        LOD 100

        Pass
        {
            CGPROGRAM
            #pragma vertex vert
            #pragma fragment frag
            __#pragma multi_compile_instancing__
            #include "UnityCG.cginc"

            struct appdata
            {
                float4 vertex : POSITION;
                __UNITY_VERTEX_INPUT_INSTANCE_ID__
            };

            struct v2f
            {
                float4 vertex : SV_POSITION;
                __UNITY_VERTEX_INPUT_INSTANCE_ID // necessary only if you want to access instanced properties in fragment Shader.__
            };

            __UNITY_INSTANCING_CBUFFER_START(MyProperties)__
                __UNITY_DEFINE_INSTANCED_PROP(float4, _Color)__
            __UNITY_INSTANCING_CBUFFER_END__
           
            v2f vert(appdata v)
            {
                v2f o;

                __UNITY_SETUP_INSTANCE_ID(v);__
                __UNITY_TRANSFER_INSTANCE_ID(v, o); // necessary only if you want to access instanced properties in the fragment Shader.__

                o.vertex = UnityObjectToClipPos(v.vertex);
                return o;
            }
           
            fixed4 frag(v2f i) : SV_Target
            {
                __UNITY_SETUP_INSTANCE_ID(i); // necessary only if any instanced properties are going to be accessed in the fragment Shader.__
                return __UNITY_ACCESS_INSTANCED_PROP(_Color)__;
            }
            ENDCG
        }
    }
}
```

## Shader modifications

| Addition| Function |
|:---|:---| 
| `#pragma multi_compile_instancing`| Use this to instruct Unity to generate instancing variants. It is not necessary for surface Shaders. |
| `UNITY_VERTEX_INPUT_INSTANCE_ID`| Use this in the vertex Shader input/output structure to define an instance ID. See `SV_InstanceID` for more information. |
| `UNITY_INSTANCING_CBUFFER_START(name)` / `UNITY_INSTANCING_CBUFFER_EN`D| Every per-instance property must be defined in a specially named constant buffer. Use this pair of macros to wrap the properties you want to be made unique to each instance. |
| `UNITY_DEFINE_INSTANCED_PROP(float4, _Color)`  | Use this to define a per-instance Shader property with a type and a name. In this example, the `_Color` property is unique. |
| `UNITY_SETUP_INSTANCE_ID(v);`| Use this to make the instance ID accessible to Shader functions. It must be used at the very beginning of a vertex Shader, and is optional for fragment Shaders. |
| `UNITY_TRANSFER_INSTANCE_ID(v, o);`| Use this to copy the instance ID from the input structure to the output structure in the vertex Shader. This is only necessary if you need to access per-instance data in the fragment Shader. |
| `UNITY_ACCESS_INSTANCED_PROP(color)`| Use this to access a per-instance Shader property. It uses an instance ID to index into the instance data array. |




**Notes**: 

* When using multiple per-instance properties, you don’t need to fill all of them in `MaterialPropertyBlocks`.

* If one instance lacks the property, Unity takes the default value from the referenced Material. If the material does not have a default value for the specified property, Unity sets the value to 0. Do not put non-instanced properties in the `MaterialPropertyBlock`, because this disables instancing. Instead, create different Materials for them.




## Advanced GPU instancing tips

### Batching priority

When batching, Unity prioritizes [Static batching](DrawCallBatching) over instancing. If you mark one of your GameObjects for static batching, and Unity successfully batches it, Unity disables instancing on that GameObject, even if its Renderer uses an instancing Shader. When this happens, the Inspector window displays a warning message suggesting that you disable Static Batching. To do this, open the Player Settings (__Edit__ > __Project Settings__ > __Player__), open __Other Settings__, and under the __Rendering__ section, untick the __Static Batching__ checkbox.

Unity prioritizes instancing over dynamic batching. If Unity can instance a Mesh, it disables dynamic batching for that Mesh.

### Graphics.DrawMeshInstanced

Some factors can prevent GameObjects from being instanced together automatically. These factors include Material changes and depth sorting. Use [Graphics.DrawMeshInstanced](Graphics.DrawMeshInstanced.html) to force Unity to draw these objects using GPU instancing. Like [Graphics.DrawMesh](ScriptRef:Graphics.DrawMesh.html), this function draws Meshes for one frame without creating unnecessary GameObjects. 

Do not submit batches of instances that exceed the `maxcount` specified in your Shader script (500 by default). When using graphics tools from [OpenGL](https://www.opengl.org/) or [Metal](https://developer.apple.com/metal/), Unity divides the `maxcount` by 4, and uses the result as the maximum number of batches you can submit. The recommended practice for drawing arbitrary number of instances is to maintain a pool of pre-allocated 500-sized arrays (and `MaterialPropertyBlocks` if needed) and reuse these arrays as much as possible. See documentation on [Automatic Memory Management](UnderstandingAutomaticMemoryManagement) for more information about object pooling.

### Graphics.DrawMeshInstancedIndirect

Use `DrawMeshInstancedIndirect` in a script to read the parameters of instancing draw calls, including the number of instances, from a compute buffer. This is useful if you want to populate all of the instance data from the GPU, and the CPU does not know the number of instances to draw (for example, when performing GPU culling). See API documentation on [Graphics.DrawMeshInstancedIndirect](ScriptRef:DrawMeshInstancedIndirect.html) for a detailed explanation and code examples.


### pragma instancing_options

The `#pragma instancing_options` directive can use the following switches: 

| **Switch**| **Function** |
|:---|:---| 
| `maxcount: batchSize`| Use this to specify the maximum number of instances to draw in one instanced draw call. By default this value is 500. When using OpenGL or Metal, Unity divides the `maxcount` by 4, and uses the result as the maximum number of batches you can submit. Make this value as small as possible to match the amount of instances you want to draw. For example, to draw a maximum of 1000 instances, add `maxcount: 1000` to your shader script. Larger values increase Shader compilation time, and can reduce GPU performance.|

| `force_same_maxcount_for_gl`| Use this to force Unity to stop dividing the maxcount by 4 on graphics tools from [OpenGL](https://www.opengl.org/) or [Metal](https://developer.apple.com/metal/).|

| `assumeuniformscaling`| Use this to instruct Unity to assume that all the instances have uniform scalings (the same scale for all X, Y and Z axes).|

| `lodfade`| Use this to make [LOD](LevelOfDetail) fade values instanceable. This is useful for [SpeedTree](SpeedTree) and other LOD techniques that use the LOD fading feature.|

| `procedural:FunctionName`| Use this to instruct Unity to generate an additional variant for use with [Graphics.DrawMeshInstancedIndirect](ScriptRef:DrawMeshInstancedIndirect.html). <br/>At the beginning of the vertex Shader stage, Unity calls the function specified after the colon. To set up the instance data manually, add per-instance data to this function in the same way you would normally add per-instance data to a Shader. Unity also calls this function at the beginning of a fragment Shader if any of the fetched instance properties are included in the fragment Shader. |



### UnityObjectToClipPos

When writing shader scripts, always use `UnityObjectToClipPos(v.vertex)` instead of `mul(UNITY_MATRIX_MVP,v.vertex)`. 

While you can continue to use `UNITY_MATRIX_MVP` as normal in instanced Shaders, `UnityObjectToClipPos` is the most efficient way to transform vertex positions from object space into clip space. Unity also implements a Shader upgrader that scans all your Shaders in the project, and automatically replaces any occurrence of `mul(UNITY_MATRIX_MVP, v)` with `UnityObjectToClipPos(v)`.

The console window (menu: __Window__ > __Console__) displays performance warnings if there are still places where `UNITY_MATRIX_MVP` (along with `UNITY_MATRIX_MV`) is used.

## Further notes

* Surface Shaders have instancing variants generated by default, unless you specify `noinstancing` in the `#pragma` surface directive. Standard and StandardSpecular Shaders are already modified to have instancing support, but with no per-instance properties defined other than the transforms. Unity ignores uses of `#pragma multi_compile_instancing` in a surface Shader.

* Unity strips instancing variants if GPU Instancing is not enabled on any GameObject in the Scene. To override the stripping behaviour, open the [Graphics Settings](class-GraphicsSettings) (menu: __Edit __> __Project Settings__ > __Graphics__), navigate to the __Shader stripping__ section and change the __Instancing Variants__. 

* For `Graphics.DrawMeshInstanced`, you need to enable GPU Instancing on the Material that is being passed into this method. However, `Graphics.DrawMeshInstancedIndirect` does not require you to enable GPU Instancing. The indirect instancing keyword `PROCEDURAL_INSTANCING_ON` is not affected by stripping.

* Instanced draw calls appear in the [Frame Debugger](FrameDebugger) as __Draw Mesh (instanced)__.

* You don’t always need to define per-instance properties. However, setting up an instance ID is mandatory, because world matrices need it to function correctly. Surface shaders automatically set up an instance ID. You must set up the instance ID for Custom Vertex and Fragment shaders manually. To do this, use `UNITY_SETUP_INSTANCE_ID` at the beginning of the Shader.

* When using forward rendering, Unity cannot efficiently instance objects that are affected by multiple lights. Only the base pass can make effective use of instancing, not the added passes. For more information about lighting passes, see documentation on [Forward Rendering](RenderTech-ForwardRendering) and [Pass Tags](SL-PassTags)

* Objects that use lightmaps, or are affected by different light or [Reflection Probes](class-ReflectionProbe), can’t be instanced.

* If you have more than two passes for multi-pass Shaders, only the first passes can be instanced. This is because Unity forces the later passes to be rendered together for each object, forcing Material changes.

* All the Shader macros used in the above examples are defined in *UnityInstancing.cginc*. Find this file in the following directory: *[Unity installation folder]\Editor\Data\CGIncludes*.


------

* <span class="page-edit">2017-05-18  <!-- include IncludeTextAmendPageYesEdit --></span>

* <span class="page-history">Enable instancing checkbox guidance, DrawMeshInstancedIndirect, #pragma multi-compile added in 5.6</span>
