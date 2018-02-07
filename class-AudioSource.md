Audio Source
============


The __Audio Source__ plays back an [Audio Clip](class-AudioClip) in the scene. The clip can be played to an [audio listener](class-AudioListener) or through an [audio mixer](class-AudioMixer). The audio source can play any type of [Audio Clip](class-AudioClip) and can be configured to play these as 2D, 3D, or as a mixture (_SpatialBlend_). The audio can be spread out between speakers (stereo to 7.1) (_Spread_) and morphed between 3D and 2D (_SpatialBlend_). This can be controlled over distance with falloff curves. Also, if the [listener](class-AudioListener) is within one or multiple [Reverb Zones](class-AudioReverbZone), reverberation is applied to the source. Individual filters can be applied to each audio source for an even richer audio experience. See [Audio Effects](class-AudioEffect) for more details.

![](../uploads/Main/AudioSourceInspector.png) 

Properties
----------

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Audio Clip__ |Reference to the sound clip file that will be played. |
|__Output__ |The sound can be output through an [audio listener](class-AudioListener) or an [audio mixer](class-AudioMixer). |
|__Mute__ |If enabled the sound will be playing but muted. |
|__Bypass Effects__ |This is to quickly "by-pass" filter effects applied to the audio source. An easy way to turn all effects on/off.|
|__Bypass Listener Effects__ |This is to quickly turn all Listener effects on/off.|
|__Bypass Reverb Zones__ |This is to quickly turn all Reverb Zones on/off.|
|__Play On Awake__ |If enabled, the sound will start playing the moment the scene launches. If disabled, you need to start it using the __Play()__ command from scripting. |
|__Loop__ |Enable this to make the __Audio Clip__ loop when it reaches the end. |
|__Priority__ |Determines the priority of this audio source among all the ones that coexist in the scene. (Priority: 0 = most important. 256 = least important. Default = 128.). Use 0 for music tracks to avoid it getting occasionally swapped out.|
|__Volume__ |How loud the sound is at a distance of one world unit (one meter) from the __Audio Listener__. |
|__Pitch__ |Amount of change in pitch due to slowdown/speed up of the __Audio Clip__. Value 1 is normal playback speed. |
|__Stereo Pan__ |Sets the position in the stereo field of 2D sounds. |
|__Spatial Blend__ |Sets how much the 3D engine has an effect on the audio source. |
|__Reverb Zone Mix__ |Sets the amount of the output signal that gets routed to the reverb zones. The amount is linear in the (0 - 1) range, but allows for a 10 dB amplification in the (1 - 1.1) range which can be useful to achieve the effect of near-field and distant sounds. |
|__**3D Sound Settings**__|Settings that are applied proportionally to the Spatial Blend parameter.|
|__Doppler Level__ |Determines how much doppler effect will be applied to this audio source (if is set to 0, then no effect is applied).|
|__Spread__ |Sets the spread angle to 3D stereo or multichannel sound in speaker space. |
|__Min Distance__ |Within the MinDistance, the sound will stay at loudest possible. Outside MinDistance it will begin to attenuate. Increase the MinDistance of a sound to make it 'louder' in a 3d world, and decrease it to make it 'quieter' in a 3d world.|
|__Max Distance__ |The distance where the sound stops attenuating at. Beyond this point it will stay at the volume it would be at MaxDistance units from the listener and will not attenuate any more.|
|__Rolloff Mode__ |How fast the sound fades. The higher the value, the closer the Listener has to be before hearing the sound. (This is determined by a Graph).|
|__- Logarithmic Rolloff__ |The sound is loud when you are close to the audio source, but when you get away from the object it decreases significantly fast.|
|__- Linear Rolloff__ |The further away from the audio source you go, the less you can hear it.|
|__- Custom Rolloff__ |The sound from the audio source behaves accordingly to how you set the graph of roll offs.|


Types of Rolloff
----------------

There are three Rolloff modes: Logarithmic, Linear and Custom Rolloff. The Custom Rolloff can be modified by modifying the volume distance curve as described below. If you try to modify the volume distance function when it is set to Logarithmic or Linear, the type will automatically change to Custom Rolloff.


![Rolloff Modes that an audio source can have.](../uploads/Main/TypesOfRollOff.png) 

Distance Functions
------------------


There are several properties of the audio that can be modified as a function of the distance between the audio source and the audio listener.

**Volume**: Amplitude(0.0 - 1.0) over distance. 

**Spatial Blend**: 2D (original channel mapping) to 3D (all channels downmixed to mono and attenuated according to distance and direction). 

**Spread**: Angle (degrees 0.0 - 360.0) over distance. 

**Low-Pass** (only if LowPassFilter is attached to the AudioSource): Cutoff Frequency (22000.0-10.0) over distance.

**Reverb Zone**: Amount of signal routed to the reverb zones. Note that the volume property and distance and directional attenuation are applied to the signal first and therefore affect both the direct and reverberated signals.


![Distance functions for Volume, Spatial Blend, Spread, Low-Pass audio filter, and Reverb Zone Mix. The current distance to the Audio Listener is marked in the graph by the red vertical line.](../uploads/Main/AudioDistanceFunctions.png) 

To modify the distance functions, you can edit the curves directly. For more information, see the guide to [Editing Curves](EditingCurves).

Creating Audio Sources
----------------------


Audio Sources don't do anything without an assigned __Audio Clip__. The Clip is the actual sound file that will be played back. The Source is like a controller for starting and stopping playback of that clip, and modifying other audio properties.

To create a new Audio Source:

1. Import your audio files into your Unity Project. These are now Audio Clips.
1. Go to __GameObject-&gt;Create Empty__ from the menubar.
1. With the new GameObject selected, select __Component-&gt;Audio-&gt;Audio Source__.
1. Assign the __Audio Clip__ property of the Audio Source Component in the Inspector.

**Note:** If you want to create an __Audio Source__ just for one __Audio Clip__ that you have in the Assets folder then you can just drag that clip to the scene view - a GameObject with an __Audio Source__ component will be created automatically for it. Dragging a clip onto on existing GameObject will attach the clip along with a new __Audio Source__ if there isn't one already there. If the object does already have an __Audio Source__ then the newly dragged clip will replace the one that the source currently uses.
