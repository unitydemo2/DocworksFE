## User LUT

The effect descriptions on this page refer to the default effects found within the post-processing stack.

User LUT is a simpler method of color grading where pixels on screen are replaced by new values from an LUT (or look-up texture) supplied by the user. It is a much less advanced method than the [Color Grading](PostProcessing-ColorGrading) effect. However, as this method does not require the more advanced texture formats used by Color Grading it is recommended as a fallback for platforms that do not support these formats.

![Scene with User LUT (LUT overlaid for demonstrative purposes)](../uploads/Main/PostProcessing-UserLut-0.png)

![Scene without User LUT (LUT overlaid for demonstrative purposes)](../uploads/Main/PostProcessing-UserLut-1.png)

![UI for User LUT](../uploads/Main/PostProcessing-UserLut-2.png)

### Properties

| __Property:__| __Function:__ |
|:---|:---| 
| __Lut__| Custom lookup texture (strip format, e.g. 256x16). |
| __Contribution__| Blending factor. |



### Optimisation

* If using a 1024x32 texture for input, consider using a 256x16 instead

### Details

User LUT uses a "strip format" texture for input. Two neutral LUTs are provided with the Post-processing stack, one at a resolution of 256x16 and another at 1024x32. Using larger input textures will affect performance.

To create an LUT import one of the neutral LUTs into an image editing tool such as Photoshop with a screenshot of your scene. Apply color corrections in a non destructive manner on top of these two images until you are happy with the result. Note that only pixel-local effects are supported by LUTs, meaning no blur and other effects that depends on the value of neighboring pixels. Now export the LUT with these color changes applied back into Unity to be used in the User LUT effect.

The User LUT effect will prompt you to make changes to the texture’s import settings if necessary.

You can achieve a "lo-fi" effect by manually setting the __Filter Mode__ of the input texture to __Point (no filter)__.

![Scene using the same LUT as above, but with Filter Mode set to Point](../uploads/Main/PostProcessing-UserLut-3.png)

### Requirements

* Shader model 3

See the [Graphics Hardware Capabilities and Emulation](GraphicsEmulation) page for further details and a list of compliant hardware.

---

* <span class="page-edit"> 2017-05-24  <!-- include IncludeTextNewPageNoEdit --></span>

* <span class="page-history">New feature in 5.6</span>