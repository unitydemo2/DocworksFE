#Trail Renderer

The __Trail Renderer__ is used to make trails behind GameObjects in the Scene as they move about.


![](../uploads/Main/Inspector-TrailRenderer.png)

##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Cast Shadows__ |Determines whether the trail casts shadows, whether they should be cast from one or both sides of the trail, or whether the trail should only cast shadows and not otherwise be drawn. See [Renderer.shadowCastingMode](ScriptRef:Renderer-shadowCastingMode.html) in the Scripting API reference documentation to learn more. |
|__Receive Shadows__ |If enabled, the trail receives shadows. |
|__Motion Vectors__ |If enabled, the trail has motion vectors rendered into the Camera motion vector Texture. See [Renderer.motionVectors](ScriptRef:Renderer-motionVectors) in the Scripting API reference documentation to learn more. |
|__Materials__ |These properties describe an array of Materials used for rendering the trail. Particle Shaders work best for trails.|
|__Lightmap Parameters__ |Reference a [Lightmap Parameters](LightmapParameters) Asset here to enable the trail to interact with the global illumination system.|
|__Time__ |Define the length of the trail, measured in seconds. |
|__Min Vertex Distance__ |The minimum distance between anchor points of the trail (see details below). |
|__AutoDestruct__ |Enable this to destroy the GameObject once it has been idle for __Time__ seconds. |
|__Width__ |Define a width value and a curve to control the width of your trail at various points between its start and end. The curve is applied from the beginning to the end of the trail, and sampled at each vertex. The overall width of the curve is controlled by the width value. |
|__Color__ |Define a gradient to control the color of the trail along its length. |
|__Corner Vertices__ |This property dictates how many extra vertices are used when drawing corners in a trail. Increase this value to make the trail corners appear rounder. |
|__End Cap Vertices__ |This property dictates how many extra vertices are used to create end caps on the trail. Increase this value to make the trail caps appear rounder. |
|__Alignment__ |Set to __View__ to make the Trail face the camera, or __Local__ to align it based on the orientation of its Transform component. |
|__Texture Mode__ |Control how the Texture is applied to the Trail. Use __Stretch__ to apply the Texture map along the entire length of the trail, or use __Wrap__ to repeat the Texture along the length of the Trail. Use the __Tiling__ parameters in the Material to control the repeat rate. |
|__Light Probes__ |Probe-based lighting interpolation mode.|
|__Reflection Probes__ |If enabled and reflection probes are present in the Scene, a reflection Texture is picked for this Trail Renderer and set as a built-in Shader uniform variable.|

##Details

The Trail Renderer renders a trail of polygons behind a moving GameObject. This can be used to give an emphasized feeling of motion to a moving object, or to highlight the path or position of moving objects. A trail behind a projectile adds visual clarity to its trajectory; contrails from the tip of a plane’s wings are an example of a trail effect that happens in real life.

A Trail Renderer should be the only renderer used on the attached GameObject. It is best to create an empty GameObject, and attach a Trail Renderer as the only renderer. You can then parent the Trail Renderer to whatever GameObject you would like it to follow.


###Materials

A Trail Renderer component should use a Material that has a Particle Shader. The Texture used for the Material should be of square dimensions (for example 256x256, or 512x512). The trail is rendered once for each Material present in the array.


###Minimum vertex separation

The __Min Vertex Distance__ value determines how far an object that contains a trail must travel before a segment of that trail is solidified. Low values like 0.1 create trail segments more often, creating smoother trails. Higher values like 1.5 create segments that are more jagged in appearance. There is a slight performance trade-off when using lower values/smoother trails, so try to use the largest possible value to achieve the effect you are trying to create. Additionally, wide trails may exhibit visual artifacts when the vertices are very close together and the trail changes direction significantly over a short distance.


###Hints

* Use Particle Materials with the Trail Renderer.
* Trail Renderers must be laid out over a sequence of frames; they cannot appear instantaneously.
* Trail Renderers rotate to display the face toward the camera, similar to other Particle Systems.

##Trail Renderer example setup

![A Trail Renderer component as it appears in the Inspector window, set up to create a multicoloured trail that gets thinner and then much wider ](../uploads/Main/TrailRenderer-example1.png)

![The resulting trail created by the above component setup](../uploads/Main/TrailRenderer-example2.png)


