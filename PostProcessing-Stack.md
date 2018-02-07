## Post-processing stack

The post-processing stack is an über effect that combines a complete set of effects into a single post-processing pipeline. This has a few advantages:

* Effects are always configured in the correct order

* It allows a combination of many effects into a single pass

* All effects are grouped together in the UI for a better user experience

The post-processing stack also includes a collection of [monitors](PostProcessing-Monitors) and [debug views](PostProcessing-DebugViews) to help you set up your effects correctly and debug problems in the output.

You can download the post-processing stack from the [Asset Store](https://www.assetstore.unity3d.com/en/#!/content/83912).

![Post-processing stack](../uploads/Main/PostProcessing-Stack-0.png)

For help on how to get started with the post-processing stack, see [Setting up the post-processing stack](PostProcessing-Stack-SetUp).

### Effects

* [Anti-aliasing (FXAA & TAA)](PostProcessing-Antialiasing)
* [Ambient Occlusion](PostProcessing-AmbientOcclusion)
* [Screen Space Reflection](PostProcessing-ScreenSpaceReflection)
* [Fog](PostProcessing-Fog)
* [Depth of Field](PostProcessing-DepthOfField)
* [Motion Blur](PostProcessing-MotionBlur)
* [Eye Adaptation](PostProcessing-EyeAdaptation)
* [Bloom](PostProcessing-Bloom)
* [Color Grading](PostProcessing-ColorGrading)
* [User Lut](PostProcessing-UserLut)
* [Chromatic Aberration](PostProcessing-ChromaticAberration)
* [Grain](PostProcessing-Grain)
* [Vignette](PostProcessing-Vignette)
* [Dithering](PostProcessing-Dithering)

For details about each individual effect included in the stack see the page for that effect.

### Post-processing stack version 2

For an early preview of the next version of the post processing stack, see [Post-processing Stack v2 ](https://github.com/Unity-Technologies/PostProcessing/tree/v2).

---

* <span class="page-edit"> 2017-09-04  <!-- include IncludeTextAmendPageSomeEdit --></span>

* <span class="page-history">New feature in 5.6</span>
* <span class="page-history">Added a link to the Post-processing Stack v2 GitHub branch, which is available as a preview in [2017.1](https://docs.unity3d.com/2017.1/Documentation/Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>