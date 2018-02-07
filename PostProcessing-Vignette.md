## Vignette

The effect descriptions on this page refer to the default effects found within the post-processing stack.

In Photography, vignetting is the term used for the darkening and/or desaturating towards the edges of an image compared to the center. This is usually caused by thick or stacked filters, secondary lenses, and improper lens hoods. It is also often used for artistic effect, such as to draw focus to the center of an image.

![Scene with Vignette.](../uploads/Main/PostProcessing-Vignette-0.png)

![Scene without Vignette.](../uploads/Main/PostProcessing-Vignette-1.png)

The Vignette effect in the post-processing stack comes in 2 modes

* Classic

* Masked

## Classic

Classic mode offers parametric controls for the position, shape and intensity of the Vignette. This is the most common way to use the effect.

![UI for Vignette when Classic is selected](../uploads/Main/PostProcessing-Vignette-2.png)

### Properties

| __Property:__| __Function:__ |
|:---|:---| 
| __Color__| Vignette color. Use the alpha channel for transparency. |
| __Center__| Sets the vignette center point (screen center is [0.5,0.5]). |
| __Intensity__| Amount of vignetting on screen. |
| __Smoothness__| Smoothness of the vignette borders. |
| __Roundness__| Lower values will make a more squared vignette. |
| __Rounded__| Should the vignette be perfectly round or be dependent on the current aspect ratio? |

### Optimisation

* N/A

### Requirements

* Shader model 3

See the [Graphics Hardware Capabilities and Emulation](GraphicsEmulation) page for further details and a list of compliant hardware.

## Masked

Masked mode multiplies a custom texture mask over the screen to create a Vignette effect. This mode can be used to achieve less common vignetting effects.

![UI for Vignette when Masked is selected](../uploads/Main/PostProcessing-Vignette-3.png)

### Properties

| __Property:__| __Function:__ |
|:---|:---| 
| __Color__| Vignette color. Use the alpha channel for transparency. |
| __Mask__| A black and white mask to use as a vignette. |
| __Intensity__| Mask opacity. |

### Optimisation

* N/A

### Requirements

* Shader model 3

See the [Graphics Hardware Capabilities and Emulation](GraphicsEmulation) page for further details and a list of compliant hardware. 

---

* <span class="page-edit"> 2017-05-24  <!-- include IncludeTextNewPageNoEdit --></span>

* <span class="page-history">New feature in 5.6</span>