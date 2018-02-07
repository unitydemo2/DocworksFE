# Video file compatibility

Unity can import video files of many different formats. After import a video file is stored as a [VideoClip](class-VideoClip) asset.

However, the compatibility of these varies according to which platform you are using - see the table below for a full compatibility list.

| Extension| Windows | OSX | Linux |
|:---|:---|:---|:---| 
| .asf| ✓ |  |  |
| .avi| ✓ |  |  |
| .dv| ✓ | ✓ |  |
| .m4v| ✓ | ✓ |  |
| .mov| ✓ | ✓ |  |
| .mp4| ✓ | ✓ |  |
| .mpg| ✓ | ✓ |  |
| .mpeg| ✓ | ✓ |  |
| .ogv| ✓ | ✓ | ✓ |
| .vp8| ✓ | ✓ | ✓ |
| .webm| ✓ | ✓ | ✓ |
| .wmv| ✓ |  |  |



Each of these formats can contain tracks with many different [codecs]. Each version of each platform also supports a different list of codecs, so make sure to consult the official documentation for the platform you are working on. For example, Windows and OSX both provide official documentation on their respective codec compatibility - see official [Windows](https://msdn.microsoft.com/en-us/library/windows/desktop/dd757927(v=vs.85).aspx) and [OSX](https://developer.apple.com/library/content/documentation/MacOSX/Conceptual/OSX_Technology_Overview/MediaLayer/MediaLayer.html) documentation for further compatibility information about these platforms.

If the Editor is unable to read the content of a track within a file, it produces an error message. If this happens, you must convert or re-encode the track from the source so it is usable by your Editor platform’s native libraries.

H.264 (typically in a .mp4, .m4v, or .mov format) is the optimal supported video codec because it offers the best compatibility across platforms.

[Video Clips](class-VideoClip) can also be used without transcoding by unchecking the __Transcode__ checkbox in the Video Clip importer (see documentation on [video sources] for more information). This allows you to use video files without any additional conversion, which is faster and prevents quality loss due to re-encoding. 

__Note:__ For best results, make sure to check that your video files are supported on each target platform.

---

* <span class="page-edit">2017-06-15 <!-- include IncludeTextNewPageSomeEdit --></span>

* <span class="page-history">New feature in Unity 5.6</span>