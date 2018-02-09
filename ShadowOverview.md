#Shadows

Unity's lights can cast __Shadows__ from a GameObject onto other parts of itself or onto other nearby GameObjects. Shadows add a degree of depth and realism to a Scene, because they bring out the scale and position of GameObjects that can otherwise look flat.

![Scene with GameObjects casting shadows](../uploads/Main/ShadowIntro.png)


##How do Shadows work?

Consider a simple Scene with a single light source. Light rays travel in straight lines from that source, and may eventually hit GameObjects in the Scene. Once a ray has hit a GameObject, it can't travel any further to illuminate anything else (that is, it "bounces" off the first GameObject and doesn't pass through). The shadows cast by the GameObject are simply the areas that are not illuminated because the light couldn't reach them.

![](../uploads/Main/ShadowMapIntro.svg)

Another way to look at this is to imagine a Camera at the same position as the light. The areas of the Scene that are in shadow are precisely those areas that the Camera can't see.

![A "light's eye view" of the same Scene](../uploads/Main/ShadowLightsEyeView.svg)

In fact, this is exactly how Unity determines the positions of shadows from a light. The light uses the same principle as a Camera to "render" the Scene internally from its point of view. A depth buffer system, as used by Scene Cameras, keeps track of the surfaces that are closest to the light; surfaces in a direct line of sight receive illumination but all the others are in shadow. The depth map in this case is known as a __Shadow Map__ (you may find the [Wikipedia Page](http://en.wikipedia.org/wiki/Shadow_mapping) on shadow mapping useful for further information).


##Enabling Shadows

Use the __Shadow Type__ property in the Inspector to enable and define shadows for an individual light.

![](../uploads/Main/ShadowTypeInspector.svg)

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Shadow Type__| The __Hard Shadows__ setting produces shadows with a sharp edge. Hard shadows are not particularly realistic compared to __Soft Shadows__ but they involve less processing, and are acceptable for many purposes. Soft shadows also tend to reduce the "blocky" aliasing effect from the shadow map. |
|__Strength__ | This determines how dark the shadows are. In general, some light is scattered by the atmosphere and reflected off other GameObjects, so you usually don't want shadows to be set to maximum strength. |
|__Resolution__ | This sets the rendering resolution for the shadow map's "Camera" mentioned above. If your shadows have very visible edges, then you might want to increase this value. |
|__Bias__ | Use this to fine-tune the position and definition of your shadow. See [Shadow mapping and the Bias property](#LightBias), below, for more information. |
|__Normal Bias__ | Use this to fine-tune the position and definition of your shadow. See [Shadow mapping and the Bias property](#LightBias), below, for more information. |
|__Shadow Near Plane__ | This allows you to choose the value for the near plane when rendering shadows. GameObjects closer than this distance to the light do not cast any shadows. |

Each [Mesh Renderer](class-MeshRenderer) in the Scene also has a __Cast Shadows__ and a __Receive Shadows__ property, which must be enabled as appropriate.

![](../uploads/Main/ShadowCastMeshInspector.svg)

Enable __Cast Shadows__ by selecting __On__ from the drop-down menu to enable or disable shadow casting for the mesh. Alternatively, select __Two Sided__ to allow shadows to be cast by either side of the surface (so backface culling is ignored for shadow casting purposes), or __Shadows Only__ to allow shadows to be cast by an invisible GameObject.

<a name="LightBias"></a>
##Shadow mapping and the Bias property

The shadows for a given Light are determined during the final Scene rendering. When the Scene is rendered to the main Camera view, each pixel position in the view is transformed into the coordinate system of the Light. The distance of a pixel from the Light is then compared to the corresponding pixel in the shadow map. If the pixel is more distant than the shadow map pixel, then it is presumably obscured from the Light by another GameObject and it obtains no illumination.

![Correct shadowing](../uploads/Main/ShadowBiasGood.jpg)

A surface directly illuminated by a Light sometimes appears to be partly in shadow. This is because pixels that should be exactly at the distance specified in the shadow map are sometimes calculated as being further away (this is a consequence of using shadow filtering, or a low-resolution image for the shadow map). The result is arbitrary patterns of pixels in shadow when they should really be lit, giving a visual effect known as "shadow acne".

![Shadow acne in the form of false self-shadowing artifacts](../uploads/Main/ShadowBiasAcne.jpg)

To prevent shadow acne, a __Bias__ value can be added to the distance in the shadow map to ensure that pixels on the borderline definitely pass the comparison as they should, or to ensure that while rendering into the shadow map, GameObjects can be inset a little bit along their normals. These values are set by the __Bias__ and __Normal Bias__ properties in the [Light](class-Light) Inspector window when shadows are enabled.

Do not set the __Bias__ value too high, because areas around a shadow near the GameObject casting it are sometimes falsely illuminated. This results in a disconnected shadow, making the GameObject look as if it is flying above the ground.

![A high __Bias__ value makes the shadow appear "disconnected" from the GameObject](../uploads/Main/ShadowBiasPeterPanning.jpg)

Likewise, setting the __Normal Bias__ value too high makes the shadow appear too narrow for the GameObject:

![A high __Normal Bias__ value makes the shadow shape too narrow](../uploads/Main/ShadowBiasTooThin.jpg)

In some situations, __Normal Bias__ can cause an unwanted effect called "light bleeding", where light bleeds through from nearby geometry into areas that should be shadowed. A potential solution is to open the GameObject's [Mesh Renderer](class-MeshRenderer) and change the __Cast Shadows__ property  to __Two Sided__. This can sometimes help, although it can be more resource-instensive and increase performance overhead when rendering the Scene.

The bias values for a Light may need tweaking to make sure that unwanted effects occur. It is generally easier to gauge the right value by eye rather than attempting to calculate it.

To further prevent shadow acne we are using a technique known as **Shadow pancaking** (see [Directional light shadows: Shadow pancaking](DirLightShadows)). This generally works well, but can create visual artifacts for very large triangles.

![A low __Shadow near plane offset__ value create the appearance of holes in shadows](../uploads/Main/ShadowNearOffsetTooLow.png)

Tweak the __Shadow Near Plane Offset__ property to troubleshoot this problem. Setting this value too high introduces shadow acne.

![Correct shadowing](../uploads/Main/ShadowNearOffsetOk.png)
