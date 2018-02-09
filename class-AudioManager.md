#Audio Manager

The __Audio Manager__ allows you to tweak the maximum volume of all sounds playing in the scene.
To see it choose __Edit &gt; Project Settings &gt; Audio__.

![](../uploads/Main/AudioSet.png) 


##Properties

|**_Property:_** ||**_Function:_** |
|:---|:---|:---|
|__Volume__ ||The volume of all sounds playing. |
|__Rolloff Scale__ ||Sets the global attenuation rolloff factor for Logarithmic rolloff based sources (see [Audio Source](class-AudioSource)). The higher the value the faster the volume will attenuate, conversely the lower the value, the slower it attenuate (value of 1 will simulate the "real world").|
|__Doppler Factor__ ||How audible the Doppler effect is. When it is zero it is turned off. 1 means it should be quite audible for fast moving objects. |
|__Default Speaker Mode__ ||Defines which speaker mode should be the default for your project. Default is 2 for stereo speaker setups (see [AudioSpeakerMode](ScriptRef:AudioSpeakerMode.html) in the scripting API reference for a list of modes).|
|__Sample Rate__||Output sample rate. If set to 0, the sample rate of the system will be used. Also note that this only serves as a reference as only certain platforms allow changing this, such as iOS or Android. |
|__DSP Buffer Size__||The size of the DSP buffer can be set to optimise for latency or performance|
||__Default__|Default buffer size|
||__Best Latency__|Trades off performance in favour of latency|
||__Good Latency__|Balance between latency and performance|
||__Best Performance__|Trades off latency in favour of performance|
|__Virtual Voice Count__||Number of virtual voices that the audio system manages. This value should always be larger than the number of voices played by the game. If not, warnings will be shown in the console. |
|__Real Voice Count__||Number of real voices that can be played at the same time. Every frame the loudest voices will be picked. |
|__Disable Audio__ ||Deactivates the audio system in standalone builds. Note that this also affects the audio of MovieTextures. In the editor the audio system is still on and will support previewing audio clips, but AudioSource. Play calls and playOnAwake will not be handled in order to simulate behavior of the standalone build. |

##Details

If you want to use Doppler Effect set __Doppler Factor__ to 1. Then tweak both __Speed of Sound__ and __Doppler Factor__ until you are satisfied. 
Speaker mode can be changed runtime from your application through scripting. See [Audio Settings](ScriptRef:AudioSettings.html).
