# The Light Inspector

Lights determine the shading of an object and the shadows it casts. As such, they are a fundamental part of graphical rendering. See documentation on [lighting](LightingOverview) and [Global Illumination](GlobalIllumination) for further details about lighting concepts in Unity. 

![](../uploads/Main/class-Light-0.png)

## Properties

| Property:| Function: |
|:---|:---| 
| __Type__| The current type of light. Possible values are __Directional__, __Point__, __Spot__ and __Area__ (see the [lighting overview](Lighting) for details of these types). |
| __Range__| Define how far the light emitted from the center of the object travels (__Point__ and __Spot__ lights only). |
| __Spot Angle__| Define the angle (in degrees) at the base of a spot light’s cone (__Spot__ light only). |
| __Color__| Use the color picker to set the color of the emitted light. |
| __Mode__| Specify the [Light Mode](LightModes) used to determine if and how a light is "baked". Possible modes are __Realtime__, __Mixed__ and __Baked__. See documentation on [Realtime Lighting](LightMode-Realtime), [Mixed Lighting](LightMode-Mixed), and [Baked Lighting](LightMode-Baked) for more detailed information. |
| __Intensity__| Set the brightness of the light. The default value for a __Directional__ light is 0.5. The default value for a __Point__, __Spot__ or __Area__ light is 1.  |
| __Indirect Multiplier__| Use this value to vary the intensity of indirect light. Indirect light is light that has bounced from one object to another. The __Indirect Multiplier__ defines the brightness of bounced light calculated by the global illumination (GI) system. If you set __Indirect Multiplier__ to a value lower than __1,__ the bounced light becomes dimmer with every bounce. A value higher than __1__ makes light brighter with each bounce. This is useful, for example, when a dark surface in shadow (such as the interior of a cave) needs to be brighter in order to make detail visible. Alternatively, if you want to use [Realtime Global Illumination](GlobalIllumination), but want to limit a single real-time Light so that it only emits direct light, set its __Indirect Multiplier__ to __0__. |
| __Shadow Type__| Determine whether this Light casts Hard Shadows, Soft Shadows, or no shadows at all. See documentation on [Shadows](ShadowOverview) for information on hard and soft shadows. |
|&nbsp;&nbsp;&nbsp;&nbsp;Baked Shadow Angle| If __Type__ is set to __Directional__ and __Shadow Type__ is set to __Soft Shadows__, this property adds some artificial softening to the edges of shadows and gives them a more natural look. |
|&nbsp;&nbsp;&nbsp;&nbsp;Baked Shadow Radius| If __Type__ is set to __Point__ or __Spot__ and __Shadow Type__ is set to __Soft Shadows__, this property adds some artificial softening to the edges of shadows and gives them a more natural look. |
|&nbsp;&nbsp;&nbsp;&nbsp;Realtime Shadows| These properties are available when __Shadow Type__ is set to __Hard Shadows__ or __Soft Shadows__. Use these properties to control real-time shadow rendering settings. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Strength| Use the slider to control how dark the shadows cast by this Light are, represented by a value between 0 and 1. This is set to 1 by default. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Resolution| Control the rendered resolution of shadow maps. A higher resolution increases the fidelity of shadows, but requires more GPU time and memory usage. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bias| Use the slider to control the distance at which shadows are pushed away from the light, defined as a value between 0 and 2. This is useful for avoiding false self-shadowing artifacts. See Shadow mapping and the bias property for more information. This is set to 0.05 by default. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Normal Bias| Use the slider to control distance at which the shadow casting surfaces are shrunk along the surface normal, defined as a value between 0 and 3. This is useful for avoiding false self-shadowing artifacts. See documentation on Shadow mapping and the bias property for more information. This is set to 0.4 by default.<br/> |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Near Plane| Use the slider to control the value for the near clip plane when rendering shadows, defined as a value between 0.1 and 10. This value is clamped to 0.1 units or 1% of the light’s __Range__ property, whichever is lower. This is set to 0.2 by default. |
| __Cookie__| Specify a Texture mask through which shadows are cast (for example, to create silhouettes, or patterned illumination for the Light). |
| __Draw Halo__| Tick this box to draw a spherical [Halo](class-Halo) of light with a diameter equal to the __Range__ value. You can also use the Halo component to achieve this. Note that the Halo component is drawn in addition to the halo from the Light component, and that the Halo component’s __Size__ parameter determines its radius, not its diameter. |
| __Flare__| If you want to set a [Flare](class-Flare) to be rendered at the Light’s position, place an Asset in this field to be used as its source. |
| __Render Mode__| Use this drop-down to set the rendering priority of the selected Light. This can affect lighting fidelity and performance (see *Performance Considerations,* below). |
|&nbsp;&nbsp;&nbsp;&nbsp;Auto| The rendering method is determined at run time, depending on the brightness of nearby lights and the current [Quality Settings](class-QualitySettings). |
|&nbsp;&nbsp;&nbsp;&nbsp;Important| The light is always rendered at per-pixel quality. Use __Important__ mode only for the most noticeable visual effects (for example, the headlights of a player’s car). |
|&nbsp;&nbsp;&nbsp;&nbsp;Not Important| The light is always rendered in a faster, vertex/object light mode.  |
| __Culling Mask__| Use this to selectively exclude groups of objects from being affected by the Light. For more information, see [Layers](Layers). |

## Details

If you create a Texture that contains an alpha channel and assign it to the __Cookie__ variable of the light, the cookie is projected from the light. The cookie’s alpha mask modulates the light’s brightness, creating light and dark spots on surfaces. This is a great way to add complexity or atmosphere to a scene.

All [built-in shaders](Built-inShaderGuide) in Unity seamlessly work with any type of light. However, [VertexLit](Built-inShaderGuide) shaders cannot display Cookies or Shadows.

All Lights can optionally cast Shadows. To do this, set the __Shadow Type__ property of each individual Light to either __Hard Shadows__ or __Soft Shadows__. See documentation on [Shadows](ShadowOverview) for more information.

## Directional Light Shadows

See documentation on [directional light shadows](DirLightShadows) for an in-depth explanation of how they work. Note that shadows are disabled for directional lights with cookies when forward rendering is used. It is possible to write custom shaders to enable shadows in this case; see documentation on [writing surface shaders](SL-SurfaceShaders) for further details.

## Hints

* __Spot__ lights with cookies can be extremely effective for creating the effect of light coming in from a window.
* Low-intensity point lights are good for providing depth to a Scene.
* For maximum performance, use a [VertexLit](Built-inShaderGuide) shader. This shader only does per-vertex lighting, giving a much higher throughput on low-end cards.

---

* <span class="page-edit"> 2017-06-08  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Updated in 5.6</span>