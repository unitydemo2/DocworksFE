PS Vita Video Playback
===

Unity supports the MPEG-4 AVC/H.264 standard format. For more information see the documentation at [https://psvita.scedev.net/docs/vita-en,Encoding-Users_Guide-vita,Overview/1/](https://psvita.scedev.net/docs/vita-en,Encoding-Users_Guide-vita,Overview/1/)

Full-screen and Render-to-texture video playback on Vita can be done using functions in the PSVitaVideoPlayer class.

A PS Vita sample package "Video" is available for download from within the PS Vita release notes, and has working examples of video playback both fullscreen and as a RenderTexture.

## Prerequisites

1. Video files must be placed in the ``PROJECT\Assets\StreamingAssets`` folder. See [Project Structure](PSVitaProjectStructure) for more details.
1. Specify a relative path when loading video files on the PS Vita: Raw/movie.pam.

## Fullscreen video
You can render fullscreen, in the background by:

1. Passing a null value to the render texture parameter when initializing the VideoPlayer with ``PSVitaVideoPlayer.Init``
1. Updating the VideoPlayer in ``OnPostRender`` by calling ``PSVitaVideoPlayer.Update``

## Video as RenderTexture
You can render to a Texture by:

1. Passing a render texture when initializing the VideoPlayer with ``PSVitaVideoPlayer.Init``
1. Updating the VideoPlayer in ``OnPreRender`` by calling ``PSVitaVideoPlayer.Update``


