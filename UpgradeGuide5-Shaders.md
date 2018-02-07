#Shaders in Unity 5.0

These are notes to be aware of when upgrading projects from Unity 4 to Unity 5, if your project uses custom shader code.

###Shaders no longer apply a 2x multiply of light intensity

Shaders no longer apply a 2x multiply of light intensity. Instead lights are automatically upgraded to be twice as bright. This creates more consistency and simplicity in light rigs. For example a directional light shining on a white diffuse surface will get the exact color of the light. The upgrade does not affect animation, thus if you have an animated light intensity value you must change your animation curves or script code and make them 2x as large to get the same look.

In the case of custom shaders where you define your own lighting functions, you need to remove the * 2 yourself.

````
// A common pattern in shader code that has this problem will look like this
c.rgb = s.Albedo * _LightColor0.rgb * (diff * atten * 2);
// You need to fix the code so it looks more like this
c.rgb = s.Albedo * _LightColor0.rgb * (diff * atten);
````
 
###Increased interpolator and instruction counts for some surface shaders

Built-in lighting pipeline in Unity 5 can in some cases use more texture coordinate interpolators or math instruction count (to get things like non-uniform mesh scale, dynamic GI etc. working). Some of your existing surface shaders might be running into texture coordinate or ALU instruction limits, especially if they were targeting shader model 2.0 (default). Adding "#pragma target 3.0" can work around this issue. See [http://docs.unity3d.com/Manual/SL-ShaderPrograms.html](http://docs.unity3d.com/Manual/SL-ShaderPrograms.html) for the reference.

###Non-uniform mesh scale has to be taken into account in shaders

In Unity 5.0, non-uniform meshes are not "prescaled" on the CPU anymore. This means that normal & tangent vectors can be non-normalized in the vertex shader. If you're doing manual lighting calculations there, you'd have to normalize them. If you're using Unity's surface shaders, then all necessary code will be generated for you.

###Fog handling was changed

Unity 5.0 makes built-in Fog work on Windows Phone and consoles, but in order to achieve that we've changed how Fog is done a bit. For surface shaders and fixed function shaders, nothing extra needs to be done - fog will be added automatically (you can add "nofog" to surface shader #pragma line to explicitly make it not support fog).

For manually written vertex/fragment shaders, fog does not happen automagically now. You need to add #pragma multi_compile_fog and fog handling macros to your shader code. Check out built-in shader source, for example Unlit-Normal how to do it.

###Surface shaders alpha channel change

By default all opaque surface shaders output 1.0 ("white") into alpha channel now. If you want to stop that, use "keepalpha" option on the #pragma surface line.

All alpha blended surface shaders use alpha component computed by the lighting function as blend factor now (instead of s.Alpha). If you're using custom lighting functions, you probably want to add something like "c.a = s.Alpha" towards the end of it.

###Sorting by material index has been removed

Unity no longer sorts by material index in the forward renderloop. This improves performance because more objects can be rendered without state changes between them. This breaks compatibility for content that relies on material index as a way of sorting. In 4.x a mesh with two materials would always render the first material first, and the second material second. In Unity 5 this is not the case, the order depends on what reduces the most state changes to render the scene.

###Fixed function TexGen, texture matrices and some SetTexture combiner modes were removed

Unity 5.0 removed support for this fixed function shader functionality:

- UV coordinate generation (TexGen command).
- UV transformation matrices (Matrix command on a texture property or inside a SetTexture).
- Rarely used SetTexture combiner modes: signed add (a+-b), multiply signed add (a*b+-c), multiply subtract (a*b-c), dot product (dot3, dot3rgba).

Any of the above will do nothing now, and shader inspector will show warnings about their usage. You should rewrite affected shaders using programmable vertex+fragment shaders instead. All platforms support them nowadays, and there are no advantages whatsoever to use fixed function shaders.

If you have fairly old versions of Projector or Water shader packages in your project, the shaders there might be using this functionality. Upgrade the packages to 5.0 version.

###Mixing programmable & fixed function shader parts is not allowed anymore

Mixing partially fixed function & partially programmable shaders (e.g. fixed function vertex lighting & pixel shader; or a vertex shader and texture combiners) is not supported anymore. It was never working on mobile, consoles or DirectX 11 anyway. This required changing behavior of Legacy/Reflective/VertexLit shader to not do that - it lost per-vertex specular support; on the plus side it now behaves consistently between platforms.

###D3D9 shader compiler was switched from Cg 2.2 to HLSL

Mostly this should be transparent (just result in less codegen bugs and slightly faster shaders). However HLSL compiler can be slightly more picky about syntax. Some examples:

- You need to fully initialize output variables. Use UNITY_INITIALIZE_OUTPUT helper macro, just like you would on D3D11.
- "float3(a_4_component_value)" constructors do not work. Use "a_4_component_value.xyz" instead.

###"unity_Scale" shader variable has been removed

The "unity_Scale" shader property has been removed. In 4.x unity_Scale.w was the 1 / uniform Scale of the transform, Unity 4.x only rendered non-scaled or uniformly scaled models. Other scales were performed on the CPU, which was very expensive & had an unexpected memory overhead.

In Unity 5.0 all this is done on the GPU by simply passing matrices with non-uniform scale to the shaders. Thus unity_Scale has been removed because it can not represent the full scale. In most cases where "unity_Scale" was used we recommend instead transforming to world space first. In the case of transforming normals, you always have to use normalize on the transformed normal now. In some cases this leads to slightly more expensive code in the vertex shader. 

````
// Unity 4.x
float3 norm = mul ((float3x3)UNITY_MATRIX_IT_MV, v.normal * unity_Scale.w);
// Becomes this in Unity 5.0
float3 norm = normalize(mul ((float3x3)UNITY_MATRIX_IT_MV, v.normal));
````

````
// Unity 4.x
temp.xyzw = v.vertex.xzxz * unity_Scale.xzxz * _WaveScale4 + _WaveOffset;
 
// Becomes this in Unity 5.0
float4 wpos = mul (_Object2World, v.vertex);
temp.xyzw = wpos.xzxz * _WaveScale4 + _WaveOffset;
````

###Shadows, Depth Textures and ShadowCollector passes

Forward rendered directional light shadows do not do separate "shadow collector" pass anymore. Now they calculate screenspace shadows from a camera's depth texture (just like in deferred lighting).

This means that LightMode=ShadowCollector passes in shaders aren't used for anything; you can just remove them from your shaders.

Depth texture itself is not generated using shader replacement anymore; it is rendered with ShadowCaster shader passes. This means that as long as your objects can cast proper shadows, then they will also appear in camera's depth texture properly (was very hard to do before, if you wanted custom vertex animation or funky alpha testing). It also means that Camera-DepthTexture.shader is not used for anything now. And also, all built-in shadow shaders used no backface culling; that was changed to match culling mode of regular rendering.
