# Baked lighting

Baked Lights are [Light components](class-Light) which have their __Mode__ property set to __Baked__.  

Use __Baked__ mode for Lights used for local ambience, rather than fully featured Lights. Unity pre-calculates the illumination from these Lights before run time, and does not include them in any run-time lighting calculations. This means that there is no run-time overhead for baked Lights. 

Unity bakes direct and indirect lighting from baked Lights into [light maps](LightmappingDirectional) (to illuminate static GameObjects) and [Light Probes](LightProbes) (to illuminate dynamic Light GameObjects). Baked Lights cannot emit specular lighting, even on dynamic GameObjects (see [Wikipedia: Specular highlight](https://en.wikipedia.org/wiki/Specular_highlight) for more information). Baked Lights do not change in response to actions taken by the player, or events which take place in the Scene. They are mainly useful for increasing brightness in dark areas without needing to adjust all of the lighting within a Scene. 

Baked Lights are also the only Light type for which dynamic GameObjects cannot cast shadows on other dynamic GameObjects. 

## Advantages of baked lighting

* High-quality shadows from statics GameObjects on statics GameObjects in the light map at no additional cost.

* Offers indirect lighting.

* All lighting for static GameObjects can be just one Texture fetched from the light map in the Shader.

## Disadvantages of baked lighting

* No real-time direct lighting (that is, no specular lighting effects).

* No shadows from dynamic GameObjects on static GameObjects.

* You only get low-resolution shadows from static GameObjects on dynamic GameObjects using Light Probes.

* Increased memory requirements compared to real-time lighting for the light map texture set, because light maps need to be more detailed to contain direct lighting information.

## Technical details

For baked Lights, Unity precomputes the entire light path, except for the path segment from the Camera to the Surface. See documentation on [Light Modes](LightModes) for more information about light paths.

![Baked Mode: All light paths are precomputed](../uploads/Main/LightMode-Baked-0.png)

Unity also precomputes direct baked lighting, which means that light direction information is not available to Unity at run time. Instead, a small number of Texture operations handle all light calculations for baked Lights in the Scene area. Without this information, Unity cannot carry out calculations for specular and glossy reflections. If you need specular reflections, use [Reflection Probes](class-ReflectionProbe) or use [Mixed](LightMode-Mixed) or [Realtime](LightMode-Realtime) lights. See documentation on [directional light maps](LightmappingDirectional) for more information. 

Baked Lights never illuminate dynamic GameObjects at run time. The only way for dynamic GameObjects to receive light from baked Lights is via [Light Probes](LightProbes). This is also the only difference between Baked Lights and any [Subtractive mode Mixed Lights](LightMode-Mixed-Subtractive) (except the main directional Light) which compute direct lighting on dynamic GameObjects at run time.

---

* <span class="page-edit"> 2017-06-08  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Light Modes added in 5.6</span>