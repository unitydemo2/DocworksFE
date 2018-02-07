#Screen Space Raytrace Reflection (SSRR)

SSRR allows shiny objects to reflect their surroundings more accurately than with reflection probes in some cases. SSRR reflections are dynamic, so moving objects appear in reflections. They also line up better at contact locations.


![A scene with only using reflection probes](../uploads/Main/ssrr-onlyrefprobe.png)

![Using SSRR along with reflection probes](../uploads/Main/ssrr-withrefprobe.png)

SSRR requires Deferred Shading to be used (since it needs information from the g-buffer: depth, normals, specular, smoothness, occlusion). If you are using SSAO effect too, then add it after the SSRR effect.

##Properties


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Velocity Scale__ |Higher scale makes image more likely to blur. |
|__Ray Pixels Step__ | Maximum error tolerated on a reflected object's silhouette. Decrease if you're seeing jagged edges on reflections seen in very smooth objects. The value shown in the GUI is actually the log of the real value used, so you'll see a speedup of about 2^r for setting this to r. larger = faster, smaller = better.|
|__Max Steps__ | Maximum number of steps to use when computing reflections. Increase if reflections are fading out too soon. Max Distance and Ray Pixels Step are better controls to use for adjusting performance and quality. Use Max Steps only to limit worst case performance in scenes with many shiny objects. smaller = faster, larger = better.|
|__Half Resolution__ | Should reflections be computed at half the resolution of the screen? Works best when surfaces are rough. Uncheck if reflections look too blurry or are showing bright lines at corners. check = faster, unchecked = better.|
|__Expected Object Thickness__ | How thick objects should appear in reflections, in world units. Increase if reflections are missing, decrease if characters, columns, or thin objects are casting reflections that appear too thick
|__Screen Edge Fading__ | Amount to fade out SSRR near the edge of the screen. Lower= better for still cameras, 1 = better for moving cameras.|
|__Max Distance__ | Farthest away object that can be reflected, in world units. Increase if reflections are fading out too soon. smaller = faster, larger = better (but off-screen objects can't be reflected no matter what -- tune your reflection probe boxes to make sure that they appear)
|__Fade Distance__ | Begin fading out SSR for reflections this far from the max distance in world units. Increase to fade reflections out faster.|
|__Reflection Multiplier__ | Non-physical multiplier for SSR. Use values < 1 to artificially knock down the contribution of SSR. This will darken the scene and may make some artifacts harder to see.|
|__Treat Backface Hit as Miss__ | Occasionally reflection rays will hit objects facing away from the camera. By default SSR will guess that the back of the object looks like the front, which can look decent, especially on rough surfaces. However it can also lead to obvious artifacts. Tick this checkbox to simply fall back to the reflection probes at pixels where the ray hits a backfacing surface.|
|__Suppress Backwards Rays__ | Flag for disabling tracing rays back towards the camera. Enable for a performance gain in scenes where most glossy objects are horizontal, like floors, water, and tables. Leave off for scenes with glossy vertical objects.|
|__Use HDR Intermediates__ | Use high-dynamic range buffers when calculating the mirror reflection and roughness convolved buffers. Enable for better reflections of very bright objects at a performance cost, if you are using an HDR GBuffer. If you are not, enabling this will bring no quality improvement.|
|__Min Smoothness__ | Very rough surfaces can flicker using SSR, due to the heavy filtering we must do to convolve the information in realtime. Increase min smoothness to have these surfaces fallback to reflection probes.|
|__Smoothness Falloff Range__ | How soon before we reach min smoothness to start falling back to reflection probes. We start falling back to non-SSR value solution at minSmoothness - smoothnessFalloffRange, with full fallback occuring at minSmoothness.|
|__Distance Blur__ | Physically correct reflections will have a smaller lobe of contributions in screen space as the reflection hit point increases in distance from the camera. Conversely, the farther from the initial surface the reflected surface is, the larger the cone of contribution. When distance blur is 0, we ignore both of these effects (which cancel out in certain cases), and when distance blur is 1 we fully take into account both effects. Intermediate values blend between both methods.|
|__Fresnel Fade__ | Amplify Fresnel fade out. Increase if floor reflections look good close to the surface and bad farther 'under' the floor.|
|__Fresnel Fade Power__ | Higher values correspond to a faster Fresnel fade as the reflection changes from the grazing angle.|
|__Bilateral Upsample__ | Content-aware upsampling for rough reflection information (and sharp reflections when doing a low-resolution trace). Improves quality significantly, especially for half-resolution tracing, at the expense of some computation time.|
|__Full Resolution Resolve__ | Compute the final reflection buffer at full resolution, even if half resolution ray tracing is enabled. This drastically increases quality on mixed-smoothness scenes when half resolution tracing is used, at the expense of some computation time.|
|__Trace Everywhere__ | When enabled, trace rays even from surfaces too rough to receive screen space reflections. Then the results can be used by neighboring pixels with smoother materials. enabled = potentially better on mixed-smoothness scenes, disabled = faster.|
|__Improve Corners__ | Avoid blurring reflections between objects and across corners in the 3D scene. enabled = better, disabled = faster.|
|__Reduce Banding__ | Smooth out the reflections of individual objects when using large steps. Does nothing when Ray Pixels Step is 1. enabled = better for smooth objects, disabled = faster.|
|__Additive Reflection__ | Add the reflections from both probes and SSRR. This gives an image that is too bright and that has ghost reflections on very smooth objects. enable = if you like the result or encounter too many motion artifacts. disable = more physically correct.|


##Recommended Settings

|**&nbsp;** | **_Performance_** | **_Default_** | **_Quality_**|
|:---|:---|:---|:---|
|Max Steps                  | 64   | 128  | 512  |
|Ray Pixels Step            | 4    | 3    | 1    |
|Wall Thickness             | 0.5m | 0.5m | 0.5m |
|Screen Edge Fading         | 0    | 0.03 | 0.03 |
|Max Distance               | 10m  | 100m | 100m |
|Fade Distance              | 10m  | 100m | 100m |
|Reflection Multiplier      | 1    | 1    | 1    |
|Treat Backface Hit as Miss | n    | n    | n    |
|Suppress Backwards Rays    | Y    | n    | n    |
|Use HDR Intermediates      | n    | Y    | Y    |
|Min Smoothness             | 0.4  | 0.2  | 0.2  |
|Trace Everywhere           | n    | Y    | Y    |
|Distance Blur              | 1    | 1    | 1    |
|Fresnel Fade               | 0.2  | 0.2  | 0.2  |
|Half Resolution            | Y    | Y    | n    |
|Full Resolution Resolve    | n    | Y    | Y    |
|Bilateral Upsample         | n    | Y    | Y    |
|Fresnel Fade Power         | 2.0  | 2.0  | 2.0  |
|Smoothness Falloff Range   | 0.05 | 0.05 | 0.05 |
|Improve Corners            | n    | Y    | Y    |
|Reduce Banding             | n    | Y    | Y    |
|Additive Reflection        | n    | n    | n    |

You can achieve even higher quality or performance than these presets by extending some values outside of the ranges used above.


##Limitations

SSRR is limited to reflecting objects that appear on the screen. It cannot reflect objects that are off the screen to the top, bottom, or sides, or that are hidden behind other objects.

The SSRR effect replaces the reflection probes in locations where it is able to find the reflected object on screen. For the best result, combine SSRR with reflection probes. Place probes within convex areas in a scene and tune their box sizes to match the major pieces of scene geometry. This is necessary to make the transitions between SSRR and reflection probes seamless.

In the real world, reflections seen in rough objects become blurrier when they are more distant from the reflector. Reflection probes do not model this behavior. SSRR blends in this feature as distanceBlur is increased from 0 to 1. 

Rougher surfaces need to convolve incoming light over a large glossy lobe, which, when approximated by SSRR in screen-space, can mean filtering over hundreds of pixels. In order to make this viable for real-time, rough reflections are computed at low resolution, which can lead to some flicker with camera movement (though our bilateral filter and upsampling can suppress this in many cases). Counter this by setting the minimum smoothness higher to fallback to the more stable reflection probe solution.



