##Audio in Unity 5.0

These are notes to be aware of when upgrading projects from Unity 4 to Unity 5, if your project uses audio features.

###AudioClips

A number of things has changed in the AudioClip. First, there is no longer a 3D flag on the asset. This flag has been moved into the AudioSource in form of the Spatial Blend slider allowing you to, at runtime, morphing sounds from 2D to 3D. Old projects will get imported in such a way that AudioSource’s on GameObjects in the scene that have a clip assigned will get their Spatial Blend parameter set up according to the old 3D flag of the AudioClip. For obvious reasons this is not possible for scripts that dynamically assign clips to sources, so this requires manual fixing.

While the default setting for the old 3D property was true, by default in the new system, the default of the Spatial Blend parameter is set to 2D.

Finally, AudioClips can now be multi-edited.

###Format

The naming of the Format property has changed so that it reflects the method by which the data is stored rather than particular file format which deviates from platform to platform. So from now on Uncompressed refers to raw sample data, Compressed refers to a lossy compression method best suited to the platform and ADPCM refers to a lightweight (in terms of CPU) compression method that is best suited to natural audio signals which contain a fair amount of noise (footsteps, impacts, weapons etc) and are to be played in large amounts.

###Preloading and loading audio data in the background

A new feature of AudioClips is that they provide support for an option for determining whether to preload the audio data or not. Any property of the AudioClip is detached from the actual audio data loading state and can be queried at any time, so having the possibility to load on demand now helps keeping the memory usage of AudioClips low. Additionally to this AudioClips can load their audio data in the background without blocking the main game thread and causing frame drops. The load process can of course be controlled via the scripting API.

###Multi-editing
All AudioClips now support multi-editing.

###Force to Mono
The Force To Mono option now performs peak-normalization on the resulting down mix.

###GetData/SetData

These API calls are only supported by clips that are either storing the audio data uncompressed as PCM or perform the decompression at on load. In the past more clips supported this, but the pattern wasn't very clear since it depended both on the target platform and had different behavior in the editor and standalone players. As a new thing, tracker files can be decompressed as PCM data into memory too, so GetData/SetData can also be used on these.

###AudioSource pause behaviour

Pausing in Unity5 is now consistent between Play calls and PlayOneShots calls. Pausing an AudioSource pauses voices played both ways, and calling Play or PlayOneShot unpauses the AudioSource for voices played both ways too.

To assist with unpausing an AudioSource without playing the assigned clip, (useful for when there are oneshot voices playing), we have added a new function AudioSource.Unpause ().

###Audio mixer

The AudioMixer is a new feature of Unity 5 allowing complex routing of the audio data from AudioSource’s to mix groups where effects can be applied. One key difference from the Audio Filter components is that audio filters get instantiated per AudioSource and therefore are more costly in terms of CPU if a game has a large number of AudioSources with filters or if a script simply creates many instances of a GameObject containing . With the mixer it is now possible to set up a group with the same effects and simply routing the audio from the AudioSource through the shared effects resulting in lower CPU usage.

The mixer does not currently support script-based effects, but it does have a new native audio plugin API allowing developers to write high-performance effects that integrate seamlessly with the other built-in effects.

###AudioSettings

The way the audio system is configured has changed. The overall settings for setting speaker mode and DSP buffer size (i.e. latency) should still be configured in the audio project settings, and additional to these it is now also possible to configure the real and virtual voices counts. The real voice count specifies how many voices can be heard concurrently and therefore has a strong impact on the overall CPU consumption of the game. Previously this was hardcoded to 32 with some platform-specific exceptions. When the number of playing voices exceeds this number, those that are least audible will be put on hold until these voices become dominant or some of the dominant voices stop playing. These voices are simply bypassed from playing. They are not stopped, simply made inactive until there is bandwidth again. The virtual voice count defines how many voices can be managed in total, so if the number of voices playing exceeds this, the least audible voices will be stopped.

AudioSettings.outputSampleRate and AudioSettings.speakerMode can still be read from, but the setters are now deprecated, as is the SetDSPBufferSize function. As a replacement for these for audio configuration changes that need to happen at runtime there is now a structure called AudioConfiguration. This can be obtained via AudioSettings.GetConfiguration() which will return the active settings on the audio output device. Changes can be made to this structure and applied via AudioSettings.Reset() which will return a boolean result depending on the successful or failed attempt of applying the changes.

Whenever changes to the audio configuration happen, either caused by scripts via AudioSettings.Reset() or because of external events such as plugging in HDMI monitors with audio support, external sound cards or USB headsets, a user-defined callback AudioSettings.OnAudioConfigurationChanged(bool deviceChanged) will be invoked. Its argument deviceChanged will be false if the change was caused by an AudioSettings.Reset() call, and true if it was caused by an external device change (this could also be changing the sample rate of the audio device in use). The callback allows you to recreate any volatile sounds such as generated PCM clips, restore any audio state, or further adapt the audio settings through a call to AudioSettings.Reset().
