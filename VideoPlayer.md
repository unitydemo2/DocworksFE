# Video overview

Use Unity’s video system to integrate video into your game. Video footage can add realism, save on rendering complexity, or help you integrate content available externally.

To use video in Unity, import [Video Clips](class-VideoClip) and configure them using the [Video Player component](class-VideoPlayer). The system allows you to feed video footage directly into the __Texture__ parameter of any [component](UsingComponents) that has one. Unity then plays the Video on that Texture at run time.

![A Video Player component (shown in the Inspector window with a ***_Video Clip_*** assigned, right) attached to a spherical GameObject (shown in the Game view, left).](../uploads/Main/Video-0.png)

Unity’s video features include the hardware-accelerated and software decoding of [Video files](VideoSources-VideoFiles), [transparency support](VideoTransparency), multiple audio tracks, and network streaming.

**Note:** The Video Player component and Video Clip asset, introduced in Unity 5.6, supersede the earlier [Movie Textures](class-MovieTexture) feature.

---

* <span class="page-edit">2017-06-15 <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">Video player support for PS4 added in [2017.1](../Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>

* <span class="page-history">New feature in Unity 5.6</span>