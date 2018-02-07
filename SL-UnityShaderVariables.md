Built-in shader variables
=========================


Unity provides a handful of built-in global variables for your shaders: things like current object's transformation matrices, light parameters, current time and so on. You use them in [shader programs](SL-ShaderPrograms) like any other variable, the only difference is that you don't have to declare them - they are all declared in `UnityShaderVariables.cginc` include file that is included automatically.


## Transformations

All these matrices are `float4x4` type.

|                           |           |
|:---                       |:---       |
| **Name**                  | **Value** |
| UNITY\_MATRIX\_MVP        | Current model \* view \* projection matrix. |
| UNITY\_MATRIX\_MV         | Current model \* view matrix. |
| UNITY\_MATRIX\_V          | Current view matrix. |
| UNITY\_MATRIX\_P          | Current projection matrix. |
| UNITY\_MATRIX\_VP         | Current view \* projection matrix. |
| UNITY\_MATRIX\_T\_MV      | Transpose of model \* view matrix. |
| UNITY\_MATRIX\_IT\_MV     | Inverse transpose of model \* view matrix. |
|\_Object2World             | Current model matrix. |
|\_World2Object             | Inverse of current world matrix. |


## Camera and screen

These variables will correspond to the [Camera](class-Camera) that is rendering. For example during shadowmap rendering,
they will still refer to the Camera component values, and not the "virtual camera" that is used for the shadowmap projection.

|                           |           |           |
|:---                       |:---       |:---       |
| **Name**                  | **Type**  | **Value** |
|\_WorldSpaceCameraPos      |float3     | World space position of the camera. |
|\_ProjectionParams         |float4     | `x` is 1.0 (or -1.0 if currently rendering with a [flipped projection matrix](SL-PlatformDifferences)), `y` is the camera's near plane, `z` is the camera's far plane and `w` is 1/FarPlane. |
|\_ScreenParams             |float4     | `x` is the width of the camera's target texture in pixels, `y` is the height of the camera's target texture in pixels, `z` is 1.0 + 1.0/width and `w` is 1.0 + 1.0/height. |
|\_ZBufferParams            |float4     | Used to linearize Z buffer values. `x` is (1-far/near), `y` is (far/near), `z` is (x/far) and `w` is (y/far). |
| unity_OrthoParams         |float4     | `x` is orthographic camera's width, `y` is orthographic camera's height, `z` is unused and `w` is 1.0 when camera is orthographic, 0.0 when perspective. |
| unity_CameraProjection    |float4x4   | Camera's projection matrix. |
| unity_CameraInvProjection |float4x4   | Inverse of camera's projection matrix. |
| unity_CameraWorldClipPlanes[6] |float4  | Camera frustum plane world space equations, in this order: left, right, bottom, top, near, far. |


## Time

|                 |          |           |
|:---             |:---      |:---       |
| **Name**        | **Type** | **Value** |
|_Time            |float4    | Time since level load (t/20, t, t\*2, t\*3), use to animate things inside the shaders. |
|\_SinTime        |float4    | Sine of time: (t/8, t/4, t/2, t). |
|\_CosTime        |float4    | Cosine of time: (t/8, t/4, t/2, t). |
|unity\_DeltaTime |float4    | Delta time: (dt, 1/dt, smoothDt, 1/smoothDt). |


## Lighting

Light parameters are passed to shaders in different ways depending on which [Rendering Path](RenderingPaths) is used,
and which LightMode [Pass Tag](SL-PassTags) is used in the shader.

[Forward rendering](RenderTech-ForwardRendering) (`ForwardBase` and `ForwardAdd` pass types):

|                                              |          |             |
|:---                                          |:---      |:---         |
| **Name**                                     | **Type** | **Value**   |
|\_LightColor0 *(declared in Lighting.cginc)*   | fixed4   |Light color. |
|\_WorldSpaceLightPos0                          | float4   |Directional lights: (world space direction, 0). Other lights: (world space position, 1). |
|\_LightMatrix0 *(declared in AutoLight.cginc)* | float4x4 |World-to-light matrix. Used to sample cookie & attenuation textures. |
|unity_4LightPosX0, unity_4LightPosY0, unity_4LightPosZ0 | float4 | *(ForwardBase pass only)* world space positions of first four non-important point lights. |
|unity_4LightAtten0                            | float4   | *(ForwardBase pass only)* attenuation factors of first four non-important point lights. |
|unity_LightColor                              | half4[4] | *(ForwardBase pass only)* colors of of first four non-important point lights. |


Deferred shading and deferred lighting, used in the lighting pass shader (all declared in UnityDeferredLibrary.cginc):

|                           |          |           |
|:---                       |:---      |:---       |
| **Name**                  | **Type** | **Value** |
|\_LightColor                | float4 | Light color. |
|\_LightMatrix0              | float4x4 |World-to-light matrix. Used to sample cookie & attenuation textures. |


Spherical harmonics coefficients (used by ambient and light probes) are set up for `ForwardBase`, `PrePassFinal` and `Deferred`
pass types. They contain 3rd order SH to be evaluated by world space normal (see `ShadeSH9` from [UnityCG.cginc](SL-BuiltinIncludes)).
The variables are all half4 type, `unity_SHAr` and similar names.


[Vertex-lit rendering](RenderTech-VertexLit) (`Vertex` pass type):

Up to 8 lights are set up for a `Vertex` pass type; always sorted starting from the brightest one. So if you want
to render objects affected by two lights at once, you can just take first two entries in the arrays. If there are less
lights affecting the object than 8, the rest will have their color set to black.

|                            |           |             |
|:---                        |:---       |:---         |
| **Name**                   | **Type**  | **Value**   |
|unity_LightColor            | half4[8]  | Light colors. |
|unity_LightPosition         | float4[8] | View-space light positions. (-direction,0) for directional lights; (position,1) for point/spot lights. |
|unity_LightAtten            | half4[8]  | Light attenuation factors. _x_ is cos(spotAngle/2) or -1 for non-spot lights; _y_ is 1/cos(spotAngle/4) or 1 for non-spot lights; _z_ is quadratic attenuation; _w_ is squared light range. |
|unity_SpotDirection         | float4[8] | View-space spot light positions; (0,0,1,0) for non-spot lights. |



## Fog and Ambient

|                           |          |           |
|:---                       |:---      |:---       |
| **Name**                  | **Type** | **Value** |
|unity_AmbientSky           |fixed4    | Sky ambient lighting color in gradient ambient lighting case. |
|unity_AmbientEquator        |fixed4    | Equator ambient lighting color in gradient ambient lighting case. |
|unity_AmbientGround        |fixed4    | Ground ambient lighting color in gradient ambient lighting case. |
|UNITY_LIGHTMODEL_AMBIENT   |fixed4    | Ambient lighting color (sky color in gradient ambient case). Legacy variable. |
|unity_FogColor             |fixed4    | Fog color. |
|unity_FogParams            |float4    | Parameters for fog calculation: (density / sqrt(ln(2)), density / ln(2), -1/(end-start), end/(end-start)). _x_ is useful for Exp2 fog mode, _y_ for Exp mode, _z_ and _w_ for Linear mode. |


##Various

|               |          |           |
|:---           |:---      |:---       |
| **Name**      | **Type** | **Value** |
|unity_LODFade  |float4    | Level-of-detail fade when using [LODGroup](class-LODGroup). _x_ is fade (0..1), _y_ is fade quantized to 16 levels, _z_ and _w_ unused. |
