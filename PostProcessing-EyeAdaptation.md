## Eye Adaptation

The effect descriptions on this page refer to the default effects found within the post-processing stack.

In ocular physiology, adaptation is the ability of the eye to adjust to various levels of darkness and light. The human eye can function from very dark to very bright levels of light. However, in any given moment of time, the eye can only sense a contrast ratio of roughly one millionth of the total range. What enables the wider reach is that the eye adapts its definition of what is black.

This effect dynamically adjusts the exposure of the image according to the range of brightness levels it contains. The adjustment takes place gradually over a period of time, so the player can be briefly dazzled by bright outdoor light when, say, emerging from a dark tunnel. Equally, when moving from a bright scene to a dark one, the "eye" takes some time to adjust.

Internally, this effect generates a histogram on every frame and filters it to find the average luminance value. This histogram, and as such the effect, requires [Compute shader](ComputeShaders) support.

![Scene with Eye Adaptation.](../uploads/Main/PostProcessing-EyeAdaptation-0.png)

![Scene without Eye Adaptation.](../uploads/Main/PostProcessing-EyeAdaptation-1.png)

![UI for Eye Adaptation](../uploads/Main/PostProcessing-EyeAdaptation-2.png)

### Properties

| __Property:__| __Function:__ |
|:---|:---| 
| Luminosity Range ||
| __Minimum (EV)__ | Lower bound for the brightness range of the generated histogram (in EV). The bigger the spread between min & max, the lower the precision will be. |
| __Maximum (EV)__| Upper bound for the brightness range of the generated histogram (in EV). The bigger the spread between min & max, the lower the precision will be. |
| Auto exposure ||
| __Histogram Filtering__| These values are the lower and upper percentages of the histogram that will be used to find a stable average luminance. Values outside of this range will be discarded and wont contribute to the average luminance. |
| __Minimum (EV)__| Minimum average luminance to consider for auto exposure (in EV). |
| __Maximum (EV)__| Maximum average luminance to consider for auto exposure (in EV). |
| __Dynamic Key Value__| Set this to true to let Unity handle the key value automatically based on average luminance. |
| __Key Value__| Exposure bias. Use this to offset the global exposure of the scene. |
| Adaptation ||
| __Adaptation Type__| Use Progressive if you want the auto exposure to be animated. Use Fixed otherwise. |
| __Speed Up__| Adaptation speed from a dark to a light environment. |
| __Speed Down__| Adaptation speed from a light to a dark environment. |



### Details

The __Luminosity Range__ __Minimum/Maximum__ values are used to set the available histogram range in EV units. The larger the range is, the less precise it will be. The default values should work fine for most cases, but if you're working with a very dark scene you'll probably want to drop both values to focus on darker areas.

Use the __Histogram Filtering__ range to exclude the darkest and brightest part of the image. To compute an average luminance you generally don't want very dark and very bright pixels to contribute too much to the result. Values are in percent.

__Auto Exposure Minimum/Maximum__ values clamp the computed average luminance into a given range.

Tweak Exposure Compensation (also known as __Key Value__) to adjust the luminance offset.

You can also set the __Adaptation Type__ to __Fixed __if you don't need the eye adaptation effect and it will behave like an auto-exposure setting.

It is recommended to use the Eye Adaptation [Debug view](PostProcessing-DebugViews) when setting up this effect.

### Requirements

* [Compute shader](ComputeShaders)

* Shader model 5

See the [Graphics Hardware Capabilities and Emulation](GraphicsEmulation) page for further details and a list of compliant hardware.

---

* <span class="page-edit"> 2017-05-24  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">New feature in 5.6</span>