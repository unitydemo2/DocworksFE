#Using Audio In WebGL

Audio in WebGL is done differently then on all other platforms. On other platforms we use FMOD internally to supply audio playback and mixing. Since the WebGL platform does not support threads, we need to use a different implementation, which is internally based on the Web Audio API, which lets the browser handle audio playback and mixing for us.

Unfortunately, this limits audio functionality in Unity WebGL to supporting only the most basic features. This page will document what is expected to work. Anything not listed here is not currently supported on WebGL.

##AudioSource

Audio sources support basic positional audio playback with pausing and resuming, panning, rolloff, pitch setting, and doppler effect support. 

The following __[`AudioSource`](ScriptRef:AudioSource.html)__ APIs are supported:

Properties:

* __[`clip`](ScriptRef:AudioSource-clip.html)__
* __[`dopplerLevel`](ScriptRef:AudioSource-dopplerLevel.html)__
* __[`ignoreListenerPause`](ScriptRef:AudioSource-ignoreListenerPause.html)__
* __[`ignoreListenerVolume`](ScriptRef:AudioSource-ignoreListenerVolume.html)__
* __[`isPlaying`](ScriptRef:AudioSource-isPlaying.html)__
* __[`loop`](ScriptRef:AudioSource-loop.html)__
* __[`maxDistance`](ScriptRef:AudioSource-maxDistance.html)__
* __[`minDistance`](ScriptRef:AudioSource-minDistance.html)__
* __[`mute`](ScriptRef:AudioSource-mute.html)__
* __[`pitch`](ScriptRef:AudioSource-pitch.html)__ (Note that only positive values for pitch are supported.)
* __[`playOnAwake`](ScriptRef:AudioSource-playOnAwake.html)__
* __[`rolloffMode`](ScriptRef:AudioSource-rolloffMode.html)__
* __[`time`](ScriptRef:AudioSource-time.html)__
* __[`timeSamples`](ScriptRef:AudioSource-timeSamples.html)__
* __[`velocityUpdateMode`](ScriptRef:AudioSource-velocityUpdateMode.html)__
* __[`volume`](ScriptRef:AudioSource-volume.html)__

Methods:

* __[`Pause`](ScriptRef:AudioSource.Pause.html)__
* __[`Play`](ScriptRef:AudioSource.Play.html)__
* __[`PlayDelayed`](ScriptRef:AudioSource.PlayDelayed.html)__
* __[`PlayOneShot`](ScriptRef:AudioSource.PlayOneShot.html)__
* __[`PlayScheduled`](ScriptRef:AudioSource.PlayScheduled.html)__
* __[`SetScheduledEndTime`](ScriptRef:AudioSource.SetScheduledEndTime.html)__
* __[`SetScheduledStartTime`](ScriptRef:AudioSource.SetScheduledStartTime.html)__
* __[`Stop`](ScriptRef:AudioSource.Stop.html)__
* __[`UnPause`](ScriptRef:AudioSource.UnPause.html)__
* __[`PlayClipAtPoint`](ScriptRef:AudioSource.PlayClipAtPoint.html)__

##AudioListener

All __[`AudioListener`](ScriptRef:AudioListener.html)__ APIs are supported.

##AudioClip

Audio clips in WebGL will always be imported in the AAC format, as that is widely supported by different browsers.

The following All __[`AudioClip`](ScriptRef:AudioClip.html)__ APIs are supported.
 APIs are supported:

Properties:

* __[`length`](ScriptRef:AudioClip-length.html)__
* __[`loadState`](ScriptRef:AudioClip-loadState.html)__
* __[`samples`](ScriptRef:AudioClip-samples.html)__

Methods:

* __[`Create`](ScriptRef:AudioClip.Create.html)__. `AudioClip.Create` is supported partially: it will only work if the streaming parameter is set to false and the complete audio samples can be loaded at the time AudioClip.Create is called. It will then create the clip and load all samples before returning control.
* __[`SetData`](ScriptRef:AudioClip.SetData.html)__. `AudioClip.SetData` is supported partially: it will only work for replacing the entire contents of the AudioClip. The `offsetSamples` parameter is ignored.

##WWW.audioClip

__[`WWW.audioClip`](ScriptRef:WWW-audioClip.html)__ should work in WebGL, if the audio clip is in a format which is natively supported by the browser. See [here](https://developer.mozilla.org/en-US/docs/Web/HTML/Supported_media_formats) for a list of supported formats in different browsers.

##Microphone

The __[`Microphone`](ScriptRef:Microphone.html)__ class is not supported in WebGL.