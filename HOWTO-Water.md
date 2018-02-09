#Water in Unity

Unity includes several water Prefabs (including the necessary Shaders, scripts and art Assets) within the [Standard Assets packages](HOWTO-InstallStandardAssets). Separate daylight and nighttime water Prefabs are provided.


![Reflective daylight water](../uploads/Main/Water_Reflective.png) 


![Reflective/Refractive daylight water](../uploads/Main/Water_ReflectiveRefractive.png) 

##Setting up water

Place one of the existing water Prefabs into your Scene. Make sure you have the [Standard Assets installed](HOWTO-InstallStandardAssets):

* Simple __Daylight Simple Water__ and __Nighttime Simple Water__ in __Standard Assets__ > __Water__.
* Fancier water - __Daylight Water__ and __Nighttime Water__ in __Pro Standard Assets__ > __Water__ (this needs some Assets from __Standard Assets__ > __Water__ as well). Water mode (Simple, Reflective, Refractive) can be set in the Inspector.

The Prefab uses an oval-shaped Mesh for the water. If you need to use a different [Mesh](class-Mesh), change it in the __Mesh Filter__ of the water GameObject:

![](../uploads/Main/Water_ChangeMesh.png) 

##Creating water from scratch (Advanced)

Simple water requires attaching a script to a plane-like mesh and using the water shader:

1. Have mesh for the water. This should be a flat mesh, oriented horizontally. UV coordinates are not required. The water GameObject should use the Water __Layer__, which you can set in the Inspector.
1. Attach the __WaterSimple__ script (from __Standard Assets/Water/Sources__) to the GameObject.
1. Use the __FX/Water (simple)__ Shader in the Material, or tweak one of the provided water Materials (__Daylight Simple Water__ or __Nighttime Simple Water__).

Reflective/refractive water requires similar steps to set up from scratch:

1. Create a Mesh for the water. This should be a flat Mesh, oriented horizontally. UV coordinates are not required. The water GameObject should use the water __Layer__, which you can set in the Inspector.
1. Attach the __Water__ script (from __Pro Standard Assets/Water/Sources__) to the GameObject (Water rendering mode can be set in the Inspector: __Simple__, __Reflective__ or __Refractive__.)
1. Use the __FX/Water__ Shader in the Material, or tweak one of the provided water Materials (__Daylight Water__ or __Nighttime Water__).


##Properties in water Materials

These properties are used in the __Reflective__ and __Refractive__ water Shaders. Most of them are used in the __Simple__ water Shader as well.


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Wave scale__ |Scaling of waves normal map. The smaller the value, the larger water waves. |
|__Reflection/refraction distort__ |How much reflection/refraction is distorted by the waves normal map. |
|__Refraction color__ |Additional tint for refraction. |
|__Environment reflection/refraction__ |Render textures for real-time reflection and refraction. |
|__Normalmap__ |Defines the shape of the waves. The final waves are produced by combining these two normal maps, each scrolling at different direction, scale and speed. The second normal map is half as large as the first one. |
|__Wave speed__ |Scrolling speed for first normal map (1st and 2nd numbers) and the second normal map (3rd and 4th numbers). |
|__Fresnel__ |A texture with alpha channel controlling the Fresnel effect - how much reflection vs. refraction is visible, based on viewing angle. |

The rest of the properties are not used by the __Reflective__ and __Refractive__ Shaders, but need to be set up in case the user's video card does not support it and must fallback to the simpler shader:


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Reflective color/cube and fresnel__ |A texture that defines water color (RGB) and Fresnel effect (A) based on viewing angle. |
|__Horizon color__ |The color of the water at horizon. `this is only used in the __Simple__ water Shader. |
|__Fallback texture__ |Define the fallback Texture used to represent the water on really old video cards, if none of the better looking Shaders can run. |
