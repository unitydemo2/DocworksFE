## Anti-aliasing

The effect descriptions on this page refer to the default effects found within the post-processing stack.

The __Anti-aliasing__ effect offers a set of algorithms designed to prevent aliasing and give a smoother appearance to graphics. Aliasing is an effect where lines appear jagged or have a "staircase" appearance (as displayed in the left-hand image below). This can happen if the graphics output device does not have a high enough resolution to display a straight line.

__Anti-aliasing__ reduces the prominence of these jagged lines by surrounding them with intermediate shades of color. Although this reduces the jagged appearance of the lines, it also makes them blurrier.

![The Scene on the left is rendered without anti-aliasing. The Scene on the right shows the effect of the Temporal Anti-aliasing algorithm.](../uploads/Main/PostProcessing-Antialiasing-0.png)

The Anti-aliasing algorithms are image-based. This is very useful when traditional multisampling (as used in the Editor’s [Quality settings](class-QualitySettings)) is not properly supported, such as:

* When using [deferred rendering](RenderTech-DeferredShading)

* When using HDR in the forward rendering path in Unity 5.5 or earlier

The algorithms supplied in the post-processing stack are:

* Fast Approximate Anti-aliasing (FXAA)

* Temporal Anti-aliasing (TAA) 

## Fast Approximate Anti-aliasing

FXAA is the cheapest technique and is recommended for mobile and other platforms that don’t support motion vectors, which are required for TAA. However it contains multiple quality presets and as such is also suitable as a fallback solution for slower desktop and console hardware.

![UI for the Anti-aliasing effect when FXAA is selected](../uploads/Main/PostProcessing-Antialiasing-1.png)

### Properties

| __Property:__| __Function:__ |
|:---|:---| 
| __Preset__| The quality preset to be used. Provides a trade-off between performance and edge quality. |

### Optimisation

* Reduce quality setting

### Requirements

* Shader model 3

See the [Graphics Hardware Capabilities and Emulation](GraphicsEmulation) page for further details and a list of compliant hardware.

## Temporal Anti-aliasing

Temporal Anti-aliasing is a more advanced anti-aliasing technique where frames are accumulated over time in a history buffer to be used to smooth edges more effectively. It is substantially better at smoothing edges in motion but requires motion vectors and is more expensive than FXAA. Due to this it is recommended for desktop and console platforms.

![UI for the Anti-aliasing effect when TAA is selected](../uploads/Main/PostProcessing-Antialiasing-2.png)

### Properties

| __Property:__| __Function:__ |
|:---|:---| 
| __Jitter - Spread__| The diameter (in texels) inside which jitter samples are spread. Smaller values result in crisper but more aliased output, whilst larger values result in more stable but blurrier output. |
| __Blending - Stationary__| The blend coefficient for stationary fragments. Controls the percentage of history sample blended into final color for fragments with minimal active motion. |
| __Blending - Motion__| The blending coefficient for moving fragments. Controls the percentage of history sample blended into the final color for fragments with significant active motion. |
| __Sharpen__| TAA can induce a slight loss of details in high frequency regions. Sharpening alleviates this issue. |



### Restrictions

* Unsupported in VR

### Requirements

* Motion vectors

* Depth texture

* Shader model 3

See the [Graphics Hardware Capabilities and Emulation](GraphicsEmulation) page for further details and a list of compliant hardware.

---

* <span class="page-edit"> 2017-05-24  <!-- include IncludeTextNewPageNoEdit --></span>

* <span class="page-history">New feature in 5.6</span>
