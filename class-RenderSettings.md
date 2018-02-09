#Scene Render Settings

The __Scene Render Settings__ (menu: __Edit &gt; Scene Render Settings__) contain default values for a range of visual elements in your scene, like [Lights](LightingOverview) and  [Skyboxes](class-Skybox).

![](../uploads/Main/SceneRenderSettings.png) 


##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|**Fog Settings** ||
|__Use Fog__ |If enabled, fog will be drawn throughout your scene. |
|__Fog Color__ |Color of the fog. |
|__Fog Mode__ |Fog mode: Linear, Exponential (Exp) or Exponential Squared (Exp2). This controls the way fog fades in with distance. |
|__Fog Density__ |Density of the fog; only used by Exp and Exp2 fog modes. |
|__Linear Fog Start/End__ |Start and End distances of the fog; only used by Linear fog mode. |
|**Environment Settings** ||
|__Skybox Material__ |Default skybox that will be rendered for cameras that have no skybox attached. |
|__Ambient Mode__ |The method of adding ambient light to the scene. The options are _Skybox_, _Sky+Equator+Ground_, _Hemisphere_ and _Flat_. |
|__Skybox Exposure__ |The degree to which the skybox affects ambient lighting. (Skybox mode only.) |
|__Create Light__ |Should Unity create a directional light that matches the skybox lighting? (Skybox mode only.) |
|__Sky Ambient__ |Color of ambient light coming from above (Sky+Equator+Ground and Hemisphere modes only.) |
|__Equator Ambient__ |Color of ambient light coming from the horizon (Sky+Equator+Ground mode only.) |
|__Ground Ambient__ |Color of ambient light coming from below (Sky+Equator+Ground and Hemisphere modes only.) |
|__Ambient Color__ |Ambient light color from all directions. (Flat mode only.) |
|__Default Reflection__ |Default reflection map for the scene, used in conjunction with [Reflection Probes](class-ReflectionProbe). The options are _Skybox_ and _Custom_. |
|__Cubemap__ |Cubemap used for reflections (only when _Default Reflection_ is set to _Custom_). |
|**Other Settings** ||
|__Halo Strength__ |Size of all light halos in relation to their __Range__. |
|__Flare Strength__ |Intensity of all flares in the scene. |
|__Flare Fade Speed__ |Time taken for flares to fade out. |
|__Halo Texture__ |Reference to a [Texture](class-TextureImporter) that will appear as the glow for all Halos in lights. |
|__Spot Cookie__ |Reference to a Texture2D that will appear as the cookie mask for all Spot lights. |


##Details

Since the Render Settings define effects like ambient light, fog and skyboxes (effects that apply to most or all objects), they strongly affect the overall look of a scene. Each scene has its own separate render settings so you can, say, have fog switched on only for outdoor scenes. A very simple preview of the settings appears at the bottom of the inspector to let you get an idea of how the finished product will look.


###Fog Settings

Fog obscures objects in the scene according to their distance from the camera until very distant objects disappear from view altogether. The settings let you choose the color of the fog and the way in which distance affects the obscuration.

Since distant objects cannot be seen through fog, they do not need to be drawn and so using fog can be a handy way to reduce rendering overhead. Note, though, that the culling of distant objects is actually determined by the camera's Far Clip Plane, not the fog itself - see the [Camera](class-Camera) component page for further details. 

Technical note: for orthographic cameras, fog is rendered uniformly because the Z coordinate of the post-perspective space is used for the fog "depth". This is not strictly accurate for an orthographic camera but it is used for its performance benefits during rendering.


###Environment Settings

The "environment" here refers to the ambient lighting and surrounding reflections available to the scene.

In the context of scene lighting, "ambient" means that the light does not come from any precise direction or source but rather represents light scattered by the atmosphere. The _Ambient Mode_ option selects how the ambient light is generated in the scene. _Skybox_ mode lets the skybox influence the pattern of lighting and you can optionally add a directional light that corresponds to the brightest point in the skybox image. The _Sky+Equator+Ground_ and _Hemisphere_ modes allow a different ambient light color to arrive from general directions. _Hemisphere_ uses one color for light arriving from roughly above the object and another for light that originates from beneath (reflected up from the ground). _Sky+Equator+Ground_ adds a third color for light coming from roughly the horizon level.

The _Default Reflection_ is used with [Reflection Probes](class-ReflectionProbe) as a default when an object is not within range of any probe in the scene. The default reflection can be set to use the scene skybox or any other cubemap.

###Other Settings

The remaining settings mostly affect the appearance of light flares and halos in the scene. Additionally, the _Spot Cookie_ defines a cookie that will be applied by default to all spotlights.