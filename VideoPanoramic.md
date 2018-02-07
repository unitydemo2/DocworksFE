# Panoramic video

Unity's panoramic video feature enables you to:

* Easily include real-world video shot in 360 degrees. 
* Reduce Scene complexity in VR by including a pre-rendered backdrop video instead of real geometry.

Unity supports 180 and 360 degree videos in either an [equirectangular](https://en.wikipedia.org/wiki/Equirectangular_projection) layout (longitude and latitude) or a [cubemap](https://docs.unity3d.com/2017.2/Documentation/Manual/class-Cubemap.html) layout (6 frames). 

Equirectangular 2D videos should have an aspect ratio of exactly 2:1 for 360 content, or 1:1 for 180 content.

![Equirectangular 2D video](../uploads/Main/Equirectangular2D.png)

Cubemap 2D videos should have an aspect ratio of 1:6, 3:4, 4:3, or 6:1, depending on face layout:

![Cubemap 2D video](../uploads/Main/Cubemap2D.png)

To use the panoramic video features in the Unity Editor, you must have access to panoramic video clips, or know how to author them.

This page describes the following steps to display any panoramic video in the Editor:

1. Set up a [Video Player](class-VideoPlayer) to play the video source to a [Render Texture](class-RenderTexture).

2. Set up a [Skybox](class-Skybox) Material that receives the Render Texture.

3. Set the Scene to use the Skybox Material.

**Note**: This is a resource-intensive feature. For best visual results, use panoramic videos in the highest possible resolution (often 4K or 8K). Large videos require more computing power and resources for decoding. Most systems have specific limits on maximum video decoding resolutions (for example, many mobiles are limited to HD or 2K, and older desktops might be limited to 2K or 4K).

## 1. Video player setup

Import your video into Unity as an [Asset](ImportingAssets). To create a Video Player, drag the video Asset from the Project view to an empty area of Unity's Hierarchy view. By default, this sets up the component to play the video full-screen for the default Camera. Press __Play__ to view this.

You should change this behaviour so that it renders to a Render Texture. That way, you can control exactly how it is displayed. To do this, go to __Assets__ &gt; __Create__ &gt; __Render Texture__. 

Set the Render Texture’s __Size__ to match your video exactly. To check the dimensions of your video, select the video in your Assets folder and view the Inspector window. Scroll to the section where Unity previews your video, select your video’s name in the preview window, and change it to __Source Info__.

Next, set your Render Texture’s __Depth Buffer__ option to __No depth buffer__.

![Render Texture set to **No depth buffer**](../uploads/Main/DepthBuffer.png)

Now, open the __Video Player__ Inspector and switch the __Render Mode__ to __Render Texture__. Drag your new Render Texture from the Asset view to the __Target Texture__ slot.

Enter Play mode to verify that this is functioning correctly.

The video doesn’t render in the __Game__ window, but you can select the Render Texture Asset to see that its content updating with each video frame. 

![](../uploads/Main/RenderTextureAsset.png)

## 2. Create a Skybox Material

You need to replace the default Skybox with your video content to render the panoramic video as a backdrop to your Scene.

To do this, create a new Material (__Assets__ &gt; __Create__ &gt; __Material__). Go to your new Material’s Inspector and set the Material’s Shader to Skybox/Panoramic (go to __Shader__ &gt; __Skybox__ &gt; __Panoramic__).

Drag the Render Texture from the Asset view to the Texture slot in the new Material’s Inspector.

You must correctly identify the type of content in the video (cubemap or equirectangular) for the panoramic video to display properly. For cubemap content (such as a cross and strip layout, as is common for static Skybox Textures), set __Mapping__ to __6 Frames Layout__.

For equirectangular content, set __Mapping__ to __Latitude Longitude Layout__, and then either the __360 degree__ or __180 degree__ sub-option. Choose the __360 degree__ option if the video covers a full 360-degree view. Choose __180 degree__ if the video is just a front-facing 180-degree view.

Look at the __Preview__ at the bottom of the Material Inspector. Pan around and check that the content looks correct. 

## 3. Render the panoramic video to the Skybox

Finally, you must connect your new Skybox Material to the Scene.

1. Open up the Lighting window (menu: __Window__ &gt; __Lighting__ &gt; __Settings__).

2. Drag and drop the new Skybox Material Asset to the first slot under __Environment__. 

3. Press Play to show the video as a Scene backdrop on the Skybox.

4. Change the Scene Camera orientation to show a different portion of the Skybox (and therefore a different portion of the panoramic video).

## 3D panoramic video

Turn on Virtual Reality Support in the Player Settings (menu: __Edit__ &gt; __Project Settings__ &gt; __Player__ &gt;__XR Settings__), especially if your source video has stereo content. This unlocks an extra __3D Layout__ option in the Skybox/Panoramic Material. The 3D Layout has three options : __Side by Side__, __Over__ __Under__, and __None__ (default value). 

Use the __Side by Side__ settings if the video contains the left eye's content on the left and the right eye's content on the right. Choose __Over Under__ if the left and right content are positioned above and below one another in the video. Unity detects which eye is currently being rendered and sends this information to the Skybox/Panoramic shader using [Single Pass Stereo rendering](https://docs.unity3d.com/Manual/SinglePassStereoRendering.html). The shader contains the logic to select the correct half of the video based on this information when Unity renders each eye’s content in VR.

![3D panoramic video](../uploads/Main/3dPanoramicVideo.png)

For non-360 3D video (where you shouldn’t use a Skybox Material), the same __3D Layout__ is available directly in the Video Player component when using the Camera __Near/Far__ Plane Render Modes.

## Alternate Render Texture type for cubemap videos

When working with cubemap videos, instead of the Video Player rendering to a 2D Render Texture and preserving the exact cube map layout, you can render the Video Player directly to a Render Texture Cube.

To achieve this, change the Render Texture Asset’s __Dimension__ from __2D__ to __Cube and set the Render Texture’s __Size__ to be exactly the dimensions of the individual faces of the source video. 

For example, if you have a 4 x 3 horizontal cross cubemap layout video with dimensions 4096 x 3072, set the Render Texture’s __Size__ to 1024 x 1024 (4096 / 4 and 3072 / 3).

While rendering to a Cube Target Texture, the Video Player assumes that the source video contains a cube map in either a cross or a strip layout (which it determines using the video aspect ratio). The Video Player then fills out the Render Texture’s faces with the correct cube faces.

Use the resulting Render Texture Cube as a Skybox. To do this, create a Material and assign __Skybox/Cubemap__ as the __Shader__(__Shader__ &gt; __Skybox__ &gt; __Cubemap__) instead of the Skybox/Panoramic Material described above.

## Video dimensions and transcoding

Including 3D content requires double either the width or the height of the video (corresponding to __Side-by-Side__ or __Over-Under__ layouts). 

Keep in mind that many desktop hardware video decoders are limited to 4K resolutions and mobile hardware video decoders are often limited to 2K or less which limits the resolution of playback in real-time on those platforms.

You can use video transcoding to produce lower resolution versions of panoramic videos, but take precautions to avoid introducing bleeding at the edge between left and right 3D content, or,
between cube map faces and adjacent black areas. In general, you should author video in power-of-two dimensions and transcoding to other power-of-two dimensions to reduce visual artifacts.

---

* <span class="page-edit">2017-10-25  <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Added 2D and 3D panoramic video support in  [2017.3](https://docs.unity3d.com/2017.3/Documentation/Manual/30_search.html?q=newin20173) <span class="search-words">NewIn20173</span></span>
