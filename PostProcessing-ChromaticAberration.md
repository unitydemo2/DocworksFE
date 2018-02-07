## Chromatic Aberration

The effect descriptions on this page refer to the default effects found within the post-processing stack.

In photography, chromatic aberration is an effect resulting from a camera’s lens failing to converge all colors to the same point. It appears as "fringes" of color along boundaries that separate dark and bright parts of the image.

The Chromatic Aberration effect is used to replicate this camera defect, it is also often used to artistic effect such as part of camera impact or intoxication effects. This implementation provides support for red/blue and green/purple fringing as well as user defined color fringing via an input texture.

![Scene with Chromatic Aberration](../uploads/Main/PostProcessing-ChromaticAberration-0.png)

![Scene without Chromatic Aberration](../uploads/Main/PostProcessing-ChromaticAberration-1.png)

![UI for Chromatic Aberration](../uploads/Main/PostProcessing-ChromaticAberration-2.png)

### Properties

| __Property:__| __Function:__ |
|:---|:---| 
| __Intensity__| Strength of chromatic aberrations. |
| __Spectral Texture__| Texture used for custom fringing color (will use default when empty) |



### Optimisation

* Reduce __Intensity__

### Details

Performances depend on the __Intensity __value (the higher it is, the slower the render will be as it will need more samples to render smooth chromatic aberrations).

Chromatic Aberration uses a __Spectral Texture__ input for custom fringing. Four example spectral textures are provided with the [Post-processing stack](PostProcessing-Stack):

* Red/Blue (Default)

* Blue/Red

* Green/Purple

* Purple/Green

You can create custom spectral textures in any image editing software. __Spectral Texture__ resolution is not constrained but it is recommended that they are as small as possible (such as the 3x1 textures provided).

You can achieve a less smooth effect by manually setting the __Filter Mode__ of the input texture to __Point (no filter)__.

![Scene using the same Chromatic Aberration as above, but with Filter Mode set to Point](../uploads/Main/PostProcessing-ChromaticAberration-3.png)

### Requirements

* Shader model 3

See the [Graphics Hardware Capabilities and Emulation](GraphicsEmulation) page for further details and a list of compliant hardware.

---

* <span class="page-edit"> 2017-05-24  <!-- include IncludeTextNewPageNoEdit --></span>

* <span class="page-history">New feature in 5.6</span>