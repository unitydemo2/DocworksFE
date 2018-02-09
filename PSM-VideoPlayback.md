Video Playback with Unity for PSM
===

Unity supports the MPEG-4 AVC/H.264 standard format.

Only full-screen video playback is currently supported with PSM.

## Prerequisites

1. Video files must be placed in the PROJECT\Assets\StreamingAssets folder. See [Project Structure](PSM-Features) for more details.
1. Specify a path prefixed with [Application.streamingAssetsPath](ScriptRef:Application-streamingAssetsPath.html) when loading video files on the device.
1. Videos can also be played from the ``/Documents`` ([Application.persistentDataPath](ScriptRef:Application-persistentDataPath)) and ``/Temp`` ([Application.temporaryCachePath](ScriptRef:Application-temporaryCachePath)) folders.

## Fullscreen video
1. Use the [Handheld.PlayFullScreenMovie](ScriptRef:Handheld.PlayFullScreenMovie) to initiate the playback.
1. None of the settings parameters are currently supported.
1. The video playback will end as soon as any input (button) is triggered.
