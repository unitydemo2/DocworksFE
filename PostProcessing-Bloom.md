## Bloom

The effect descriptions on this page refer to the default effects found within the post-processing stack.

Bloom is an effect used to reproduce an imaging artifact of real-world cameras. The effect produces fringes of light extending from the borders of bright areas in an image, contributing to the illusion of an extremely bright light overwhelming the camera or eye capturing the scene.

In HDR rendering a Bloom effect should only affects areas of brightness above LDR range (above 1) by setting the __Threshold __parameter just above this value.

![Scene with Bloom.](../uploads/Main/PostProcessing-Bloom-0.png)

![Scene without Bloom.](../uploads/Main/PostProcessing-Bloom-1.png)

![UI for Bloom](../uploads/Main/PostProcessing-Bloom-2.png)

### Properties

| __Property:__| __Function:__ |
|:---|:---| 
| __Intensity__| Strength of the Bloom filter. |
| __Threshold__| Filters out pixels under this level of brightness. |
| __Soft Knee__| Makes transition between under/over-threshold gradual (0 = hard threshold, 1 = soft threshold). |
| __Radius__| Changes extent of veiling effects in a screen resolution-independent fashion. |
| __Anti Flicker__| Reduces flashing noise with an additional filter. |

### Optimisation

* Reduce Radius

### Details

With properly exposed HDR scenes, __Threshold __should be set to ~1 so that only pixels with values above 1 leak into surrounding objects. You'll probably want to drop this value when working in LDR or the effect won't be visible.

__Anti Flicker__ reduces flashing noise, commonly known as "fireflies", by running an additional filter on the picture beforehand. This will affect performances and should be disabled when [Temporal Anti-aliasing](PostProcessing-Antialiasing) is enabled.

## Lens Dirt

__Lens Dirt__ applies a fullscreen layer of smudges or dust to diffract the Bloom effect. This is commonly used in modern first person shooters.

![The same scene with __Lens Dirt__ applied](../uploads/Main/PostProcessing-Bloom-3.png)

### Properties

| __Property:__| __Function:__ |
|:---|:---| 
| __Texture__| Dirtiness texture to add smudges or dust to the lens. |
| __Intensity__| Amount of lens dirtiness |



### Optimisation

* Reduce resolution of __Lens Dirt__ texture

### Details

__Lens Dirt__ requires an input texture to use as a fullscreen layer. There are four __Lens Dirt__ texture supplied in the [Post-processing stack](PostProcessing-Stack) that should cover common use cases. These textures are supplied at 3840x2160 resolution for maximum quality and should be scaled dependent on project and platform. You can create custom __Lens Dirt__ textures in any image editing software.

### Requirements

* Shader model 3

See the [Graphics Hardware Capabilities and Emulation](GraphicsEmulation) page for further details and a list of compliant hardware.

---

* <span class="page-edit"> 2017-05-24  <!-- include IncludeTextNewPageNoEdit --></span>

* <span class="page-history">New feature in 5.6</span>