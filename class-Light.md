#The Light inspector

|**5.6 DRAFT ADDITION TO DOCUMENTATION** |
|:---|
|This documentation has additional or changed information in Unity 5.6. The link below is first draft document of that addition or change. As such, the information in this document may be subject to change before final release.<br/><br/>See first draft [Light Modes](https://docs.google.com/document/d/116JvLXljfbdfllOLlyzVvWmNWpbUwcYKV16blVHuS2E/edit) documentation.|

__Lights__ are a fundamental part of graphical rendering since they determine the shading of an object and the shadows it casts. See the [Lighting](LightingOverview) and [Global Illumination](GlobalIllumination) sections of the manual for further details about lighting concepts in Unity.

![](../uploads/Main/LightInspectorV3.png) 

##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Type__ |The current type of light. Possible values are _Directional_, _Point_, _Spot_ and _Area_ (see the [Lighting Overview](Lighting) for details of these types). |
|__Baking__ |This allows you to choose if the light should be baked if Baked GI is selected. Mixed will also bake it, but it will still be present at runtime to give direct lighting to non-static objects. Realtime works both for Precomputed Realtime GI and when not using GI. See the [Global Illumination](GlobalIllumination) section of the manual for further information about lightmaps and baking. |
|__Range__ |How far light is emitted from the center of the object (Point and Spot lights only). |
|__Spot Angle__ |Determines the angle (in degrees) at the base of a spot light's cone (Spot light only). |
|__Color__ |The color of the light emitted. |
|__Intensity__ |Brightness of the light. The default value for a _Point_, _Spot_ or _Area_ light is 1 but for a _Directional_ light, it is 0.5. |
|__Bounce Intensity__ |This allows you to vary the intensity of indirect light (ie, light that is bounced from one object to another. The value is a multiple of the default brightness calculated by the GI system; if you set Bounce Intensity to a value greater than one then bounced light will be made brighter, while a value less than one will make it dimmer. This is useful, for example, when a dark surface in shadow (such as the interior of a cave) needs to be rendered brighter in order to make detail visible. Or alternatively, if you want to use Precomputed Realtime GI in general, but want to limit a single light to give direct light only, you can set its Bounce Intensity to 0.  See the [Global Illumination](GlobalIllumination) section of the manual for further information. |
|__Shadow Type__  |Determines whether _Hard Shadows_  _Soft Shadows_ or no shadows at all will be cast by this light. |
|__Baked Shadow Radius__ |If shadows are enabled then this property adds some artificial softening to the edges of shadows cast by point or spot lights (in theory, light originating from a point casts perfectly sharp shadows but this situation rarely occurs in nature). |
|__Baked Shadow Angle__ |If shadows are enabled then this property adds some artificial softening to the edges of shadows cast by directional lights (in theory, parallel light rays coming from a truly "directional" source cast perfectly sharp shadows but natural light sources don't strictly behave like this). |
|__Draw Halo__ |If checked, a spherical halo of light will be drawn with a radius equal to __Range__. See also the page about the [Halo](class-Halo) component. |
|__Flare__ |Optional reference to the [Flare](class-Flare) that will be rendered at the light's position. |
|__Render Mode__ |Importance of this light. This can affect lighting fidelity and performance, see _Performance Considerations_ below. The options are *Auto* (the rendering method is determined at runtime depending on the brightness of nearby lights and current [Quality Settings](class-QualitySettings)), *Important* (the light is always rendered at per-pixel quality and *Not Important* (the light is always rendered in a faster, vertex/object light mode). Use *Important* mode only for the most noticeable visual effects (eg, headlights of a player's car).|
|__Culling Mask__ |Use to selectively exclude groups of objects from being affected by the light; see [Layers](Layers). |


##Details

You can create a texture that contains an alpha channel and assign it to the __Cookie__ variable of the light. The Cookie will be projected from the light. The Cookie's alpha mask modulates the light amount, creating light and dark spots on surfaces. They are a great way af adding lots of complexity or atmosphere to a scene.

All [built-in shaders](Built-inShaderGuide) in Unity seamlessly work with any type of light. However, __VertexLit__ shaders cannot display Cookies or Shadows.

All Lights can optionally cast [Shadows](ShadowOverview). This is done by selecting either __Hard Shadows__ or __Soft Shadows__ for the __Shadow Type__ property of each individual Light. For more information about shadows, please read the [Shadows](ShadowOverview) page.


##Directional Light Shadows

Shadows from directional lights are explained in depth on [this page](DirLightShadows). Note that shadows are disabled for directional lights with cookies when forward rendering is used. It is, however, possible to write custom shaders to enable shadows in such a case by using the **fullforwardshadows** tag; see [this page](SL-SurfaceShaders) for further details.



##Hints

* Spot lights with cookies can be extremely effective for making light coming in from windows.
* Low-intensity point lights are good for providing depth to a scene.
* For maximum performance, use a [VertexLit](Built-inShaderGuide) shader. This shader only does per-vertex lighting, giving a much higher throughput on low-end cards.
* Auto lights can cast dynamic shadows over lightmapped objects without adding extra illumination. For this to work the Auto lights must be active when the Lightmap is baked. Otherwise they render as real time lights.
