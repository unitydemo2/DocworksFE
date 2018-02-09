## Writing post-processing effects

[Post-processing](PostProcessingOverview) is a way of applying effects to rendered images in Unity.

Any Unity [script](CreatingAndUsingScripts) that uses the  [OnRenderImage](scriptref:Camera.OnRenderImage) function can act as a post-processing effect. Add it to a [Camera](class-Camera) [GameObject](GameObjects) for the script to perform post-processing.

### OnRenderImage function

The [OnRenderImage](scriptref:Camera.OnRenderImage) Unity Scripting API function receives two arguments: 

* The source image as a [RenderTexture](class-RenderTexture) 

* The destination it should render into, which is a  RenderTexture as well.

Post-processing effects often use [Shaders](class-Shader). These read the source image, do some calculations on it, and render the result into the destination (using Graphics.Blit](ScriptRef:Graphics.Blit.html), for example). The post-processing effect fully replaces all the pixels of the destination.

Cameras can have multiple post-processing effects, each as [components](UsingComponents). Unity executes them as a stack, in the order they are listed in the [Inspector](UsingTheInspector) with the post-processing component at the top of the Inspector rendered first. In this situation, the result of the first post-processing component is passed as the "source image" to the next post-processing component. Internally, Unity creates one or more temporary render textures to keep these intermediate results in.

Note that the list of post-processing components in the post-processing stack do not specify the order they are applied in.

Things to keep in mind:

* The destination render texture can be null, which means "render to screen" (that is, the back buffer). This happens on the last post-processing effect on a Camera.

* When `OnRenderImage` finishes, Unity expects that the destination render texture is the active render target. Generally, a [Graphics.Blit](ScriptRef:Graphics.Blit.html) or manual rendering into the destination texture should be the last rendering operation.

* Turn off depth buffer writes and tests in your post-processing effect shaders. This ensures that [Graphics.Blit](ScriptRef:Graphics.Blit.html) does not write unintended values into destination Z buffer. Almost all post-processing shader passes should contain `Cull Off ZWrite Off ZTest Always` states.

* To use stencil or depth buffer values from the original scene render, explicitly bind the depth buffer from the original scene render as your depth target, using [Graphics.SetRenderTarget](ScriptRef:Graphics.SetRenderTarget.html). Pass the very first source image effects depth buffer as the depth buffer to bind.

### After opaque post-processing effects

By default, Unity executes post-processing effects after it renders a whole Scene. In some cases, you may prefer Unity to render post-processing effects after it has rendered all opaque objects in your scene but before it renders others (for example, before [skybox](class-Skybox) or [transparencies](StandardShaderMaterialParameterAlbedoColor)). Depth-based effects like Depth of Field often use this.

To do this, add an [ImageEffectOpaque](ScriptRef:ImageEffectOpaque.html) attribute on the [OnRenderImage](ScriptRef:Camera.html) Unity Scripting API function.

### Texture coordinates on different platforms

If a post-processing effect is sampling different screen-related textures at once, you might need to be aware of how different platforms use texture coordinates. A common scenario is that the effect "source" texture and camera’s [depth texture](SL-CameraDepthTexture) need different vertical coordinates, depending on anti-aliasing settings. See the Unity User Manual [Platform Differences](SL-PlatformDifferences) page for more information.

### Related topics

* [Depth Textures](SL-CameraDepthTexture) are often used in image post-processing to get distance to closest opaque surface for each pixel on screen.

* For [HDR](HDR) rendering, a [ImageEffectTransformsToLDR](ScriptRef:ImageEffectTransformsToLDR.html) attribute indicates using tonemapping.

* You can also use [Command Buffers](GraphicsCommandBuffers) to perform post-processing.

* Use [RenderTexture.GetTemporary](ScriptRef:RenderTexture.GetTemporary.html) to get temporary render textures and do calculations inside a post-processing effect.

* See also the Unity User Manual page on [Writing Shader Programs](SL-ShaderPrograms).

