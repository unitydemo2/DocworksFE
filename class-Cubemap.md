#Cubemap

A __Cubemap__ is a collection of six square textures that represent the
reflections on an environment. The six squares form the faces of an imaginary cube that surrounds an
object; each face represents the view along the directions of the world axes
(up, down, left, right, forward and back).

Cubemaps are often used to capture reflections or "surroundings" of objects; for example
[skyboxes](class-Skybox) and [environment reflections](class-ReflectionProbe) often use cubemaps.


![Cubemapped skybox and reflections](../uploads/Main/CubeMapExample.png) 


## Creating Cubemaps from Textures

Preferred way of creating cubemaps is importing them from specially laid out [textures](class-TextureImporter).
Select `Cubemap` texture import type and Unity should do the rest. Several commonly used cubemap layouts are
supported (and in most cases detected automatically).

![Cubemap texture import type](../uploads/Textures/CubeImportInspector.png)

Vertical and horizontal cross layouts, as well as column and row of cubemap faces are supported:

![](../uploads/Textures/CubeLayout6Faces.png) 

Another common layout is `LatLong` (Latitude-Longitude, sometimes called cylindrical). Panorama images are
often in this layout:

![](../uploads/Textures/CubeLayoutLatLong.png)

`SphereMap` (spherical environment map) images can also be found:

![](../uploads/Textures/CubeLayoutSphereMap.png)

By default Unity looks at the aspect ratio of the imported texture to determine the most appopriate layout from
the above. When imported, a cubemap is produced which can be used for skyboxes and reflections:

![](../uploads/Textures/CubeImportedView.png)

Selecting `Glossy Reflection` option is useful for cubemap textures that will be used by
[Reflection Probes](class-ReflectionProbe). It processed cubemap mip levels in a special way
(specular convolution) that can be used to simulate reflections from surfaces of different smoothness:

![Cubemap used in a Reflection Probe on varying-smoothness surface](../uploads/Textures/CubeOptionGlossyReflections.png)


## Legacy Cubemap Assets

Unity also supports creating cubemaps out of six separate [textures](class-TextureImporter).
Select __Assets &gt; Create &gt; Legacy &gt; Cubemap__ from the menu,
and drag six textures into empty slots in the inspector.

![Legacy Cubemap Inspector](../uploads/Main/Inspector-CubeMap.png)

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Right..Back Slots__ |Textures for the corresponding cubemap face. |
|__Face Size__ |Width and Height of each Cubemap face in pixels. The textures will be scaled automatically to fit this size. |
|__Mipmap__ |Should mipmaps be created? |
|__Linear__ |Should the cubemap use linear color? |
|__Readable__ |Should the cubemap allow scripts to access the pixel data? |

Note that it is preferred to create cubemaps using the Cubemap texture import type (see above) - this
way cubemap texture data can be compressed; edge fixups and glossy reflection convolution be performed;
and HDR cubemaps are supported.


## Other Techniques

Another useful technique is to generate the cubemap from the contents of a Unity scene using a script.
The [Camera.RenderToCubemap](ScriptRef:Camera.RenderToCubemap.html) function can record the six face
images from any desired position in the scene; the code example on the function's script reference page
adds a menu command to make this task easy.
