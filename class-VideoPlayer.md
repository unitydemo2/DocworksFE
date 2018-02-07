# Video Player component

Use the Video Player [component](Components) to attach [video files](Video) to [GameObjects](GameObjects), and play them on the GameObject’s [Texture](Textures) at run time.

The screenshot below shows a Video Player component attached to a spherical GameObject. 

By default, the __Material Property__ of a Video Player component is set to ___MainTex__, which means that when the Video Player component is attached to a GameObject that has a Renderer, it automatically assigns itself to the Texture on that Renderer (because this is the main Texture for the GameObject). Here, the GameObject has a Mesh Renderer component, so the Video Player automatically assigns it to the Renderer field, which means the Video Clip plays on the Mesh Renderer’s Texture.

![A Video Player component attached to a spherical GameObject, playing the Video Clip on the GameObject’s main Texture (in this case, the Texture of the Mesh Renderer)](../uploads/Main/Video-1.png)

You can also set a specific target for the video to play on, including:

* A [Camera](class-Camera) plane

* A [Render Texture](class-RenderTexture)

* A [Material](Materials) Texture parameter

* Any [Texture](class-TextureImporter) field in a component

## VideoPlayer component Reference

![The Video Player component](../uploads/Main/Video-2.png)


| **_Property_** | | | **_Function_** |
|:---|:---|:---|:---|
| __Source__     ||| Choose the type of source for your video. |
|| __Video Clip__ || Assign a [Video Clip](class-VideoClip) to the Video Player. |
||| __Video Clip__  | Use this field to define the Video Clip assigned to the Video Player component. Drag-and-drop the video file into this field, or click the circle to the right of the field and choose it from a list of Assets if it is in your Project folder. |
|| __URL__ || Assign a video from a URL (for example, http:// or file://). Unity reads the video from this URL at run time.  |
||| __URL__ | Enter the URL of the video you want to assign to the Video Player. |
||| __Browse...__ | Click this to quickly navigate your the local file system and open URLs that begin file://. |
| __Play On Awake__ ||| Tick the __Play On Awake__ checkbox to play the video the moment the Scene launches. Untick it if you want to trigger the video playback at another point during run time. Trigger it via scripting with the `Play()` command. |
| __Wait For First Frame__ ||| If you tick the __Wait For First Frame__ checkbox, Unity waits for the first frame of the source video to be ready for display before the game starts. If you untick it, the first few frames might be discarded to keep the video time in sync with the rest of the game. |
| __Loop__ ||| Ticking the __Loop__ checkbox to make the Video Player component loop the source video when it reaches its end. If this is unticked, the video stops playing when it reaches the end.  |
| __Playback Speed__ ||| This slider and numerical field represent a multiplier for the playback speed, as a value between 0 and 10. This is set to 1 (normal speed) by default. If the field is set to 2, the video plays at two times its normal speed. |
| __Render Mode__ ||| Use the drop-down to define how the video is rendered. |
|| __Camera Far Plane__ ||  Render the video on the Camera’s [far plane](class-Camera). |
|| __Camera Near Plane__ || Render the video on the Camera’s [near plane](class-Camera). |
||| __Camera__ | Define the [Camera](class-Camera) receiving the video. |
||| __Alpha__ | The global transparency level added to the source video. This allows elements behind the plane to be visible through it. See documentation on [video transparency support](VideoTransparency) for more information about alpha channels. |
|| __Render Texture__ || Render the video into a [Render Texture](class-RenderTexture). |
||| __Target Texture__ | Define the Render Texture where the Video Player component renders its images. |
|| __Material Override__ || Render the video into a selected Texture property of a GameObject through its Renderer’s [Material](ScriptRef:Material.html). |
||| __Renderer__ | The [Renderer](ScriptRef:Renderer.html) where the Video Player component renders its images. When set to __None__, the __Renderer__ on the same GameObject as the Video Player component is used. |
||| __Material Property__ | The name of the [Material Texture property](ScriptRef:Material.SetTexture.html) that receives the Video Player component images. |
|| __API Only__ || Render the video into the [VideoPlayer.texture](ScriptRef:Video.VideoPlayer-texture.html) Scripting API property. You must use scripting to assign the Texture to its intended destination. |
| __Aspect Ratio__ ||| The aspect ratio of the images that fill the __Camera Near Plane__, __Camera Far Plane__ or __Render Texture__ when the corresponding __Render Mode__ is used. |
|| __No Scaling__ || No scaling is used. The video is centered on the destination rectangle. |
|| __Fit Vertically__ || Scale the source to fit the destination rectangle vertically, cropping the left and right sides or leaving black areas on each side if necessary. The source aspect ratio is preserved. |
|| __Fit Horizontally__ || Scale the source to fit the destination rectangle horizontally, cropping the top and bottom regions or leaving black areas above and below if needed. The source aspect ratio is preserved. |
|| __Fit Inside__ || Scale the source to fit the destination rectangle without having to crop. Leaves black areas on the left and right or above and below as needed. The source aspect ratio is preserved. |
|| __Fit Outside__ || Scale the source to fit the destination rectangle without leaving black areas on the left and right or above and below, cropping as required. The source aspect ratio is preserved. |
|| __Stretch__ || Scale both horizontally or vertically to fit the destination rectangle. The source aspect ratio is not preserved. |
| __Audio Output Mode__ ||| Define how the source’s audio tracks are output. |
|| __None__ || Audio is not be played. |
|| __Audio Source__ || Audio samples are sent to selected [audio sources](class-AudioSource), enabling Unity’s audio processing to be applied. |
|| __Direct__ || Audio samples are sent directly to the audio output hardware, bypassing Unity’s audio processing. |
| __Controlled Tracks__ ||| The number of audio tracks in the video.<br/><br/>Only shown when __Source__ is __URL__. When __Source__ is __Video Clip__, the number of tracks is determined by examining the video file. |
| __Track Enabled__ ||| When enabled by ticking the relevant checkbox, the associated audio track is used for playback. This must be set prior to playback.<br/><br/>The text to the left of the checkbox provides information about the audio track, specifically the track number, language, and number of channels.<br/><br/>For example, in the screenshot above, this text is Track 0 [und. 1 ch]. This means it is the first track (Track 0), the language is undefined (und.), and the track has one channel (1 ch), meaning it is a mono track.<br/><br/>When the source is a URL, this information is only available during playback.<br/><br/>This property only appears if your source is a Video Clip that has an audio track (or tracks), or your source is a URL (allowing you to indicate how many tracks are expected from the URL during playback). |
|| __Audio Source__ || The [audio source](class-AudioSource) through which the audio track is played. The targeted audio source can also play Audio Clips.<br/><br/>The audio source’s playback controls (`Play On Awake` and `Play()` in scripting API) do not apply to the video source’s audio track.<br/><br/>This property only appears when the __Audio Output Mode__ is set to __Audio Source__. |
|| __Mute__ || Mute the associated audio track. In __Audio Source__ mode, the audio source’s control is used.<br/><br/>This property only appears when the __Audio Output Mode__ is set to __Direct__. |
|| __Volume__ || Volume of the associated audio track. In __Audio Source__ mode, the audio source’s volume is used.<br/><br/>This property only appears when the __Audio Output Mode__ is set to __Direct__. |

---

* <span class="page-edit">2017-06-15 <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">New feature in Unity 5.6</span>
