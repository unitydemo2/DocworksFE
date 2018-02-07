#High Dynamic Range Rendering

In standard rendering, the red, green and blue values for a pixel are each represented by a fraction in the range 0..1, where 0 represents zero intensity and 1 represents the maximum intensity for the display device. While this is straightforward to use, it doesn't accurately reflect the way that lighting works in a real life scene. The human eye tends to adjust to local lighting conditions, so an object that looks white in a dimly lit room may in fact be less bright than an object that looks grey in full daylight. Additionally, the eye is more sensitive to brightness differences at the low end of the range than at the high end.

More convincing visual effects can be achieved if the rendering is adapted to let the ranges of pixel values more accurately reflect the light levels that would be present in a real scene. Although these values will ultimately need to be mapped back to the range available on the display device, any intermediate calculations (such as Unity's image effects) will give more authentic results. Allowing the internal representation of the graphics to use values outside the 0..1 range is the essence of **High Dynamic Range (HDR)** rendering. 


##Working with HDR

HDR is enabled separately for each camera using a setting on the Camera component:

![](../uploads/Main/Camera-HDR.svg) 

When HDR is active, the scene is rendered into an HDR image buffer which can accommodate pixel values outside the 0..1 range. This buffer is then used by post-processing effects such as the [Bloom](PostProcessing-Bloom) effect in the [Post-processing stack](PostProcessing-Stack). The HDR image is then converted into the standard low dynamic range (LDR) image to be sent for display. This is usually done via Tonemapping, part of the [Color Grading](PostProcessing-ColorGrading) pipeline. The conversion to LDR must be applied at some point in the post-process pipeline but it need not be the final step if LDR-only post-processing effects are to be applied afterwards. For convenience, some post-processing effects can automatically convert to LDR after applying an HDR effect (see Scripting below).

###Tonemapping
Tonemapping is the process of mapping HDR values back into the LDR range. There are many different techniques, and what is good for one project may not be the best for another. A variety of tonemapping techniques have been included in the [Post-processing stack](PostProcessing-Stack). To use them you can download the **Post-processing stack** from the [Asset Store](https://www.assetstore.unity3d.com/en/#!/content/83912). A detailed description of the tonemapping types can be found in the [Color Grading](PostProcessing-ColorGrading) documentation.


![An exceptionally bright scene rendered in HDR. Without tonemapping, most pixels seem out of range.](../uploads/Main/WithoutTonemap.png) 


![The same scene as above. But this time, tonemapping is bringing most intensities into a more plausible range. Note that adaptive tonemapping can even blend between above and this image thus simulating the adaptive nature of capturing media (e.g. eyes, cameras).](../uploads/Main/WithTonemap.png) 


##Advantages of HDR

* Colors not being lost in high intensity areas
* Better bloom and glow support
* Reduction of banding in low frequency lighting areas


##Disadvantages of HDR

* Uses floating point render textures (rendering is slower and requires more VRAM)
* No hardware anti-aliasing support (but you can use an [Anti-Aliasing post-processing effect](PostProcessing-Antialiasing) to smooth out the edges)
* Not supported on all hardware


##Usage notes


###Forward Rendering
In forward rendering mode HDR is only supported if you have a post-processing effect present. This is due to performance considerations. If you have no post-processing effect present then no tonemapping will exist and intensity truncation will occur. In this situation the scene will be rendered directly to the backbuffer where HDR is not supported.

###Deferred Rendering
In HDR mode the lighting buffer is also allocated as a floating point buffer. This reduces banding in the lighting buffer. HDR is supported in deferred rendering even if no post-processing effects are present.

###Scripting

The __ImageEffectTransformsToLDR__ attribute can be added to a post-processing effect script to indicate that the target buffer should be in LDR instead of HDR. Essentially, this means that a script can automatically convert to LDR after applying its HDR post-processing effect. See [Writing Post-processing Effects](PostProcessingWritingEffects) for more details.

##See also

[HDR Color Picker](HDRColorPicker).


