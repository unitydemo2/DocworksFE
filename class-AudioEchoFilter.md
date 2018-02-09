#Audio Echo Filter

The __Audio Echo Filter__ repeats a sound after a given __Delay__, attenuating the repetitions based on the __Decay Ratio__.


##Properties

![](../uploads/Main/AudioEchoFilter.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Delay__ |Echo delay in ms. 10 to 5000. Default = 500.|
|__Decay Ratio__ |Echo decay per delay. 0 to 1. 1.0 = No decay, 0.0 = total decay (ie simple 1 line delay). Default = 0.5.L|
|__Wet Mix__ |Volume of echo signal to pass to output. 0.0 to 1.0. Default = 1.0.|
|__Dry Mix__ |Volume of original signal to pass to output. 0.0 to 1.0. Default = 1.0.|



##Details

The __Wet Mix__ value determines the amplitude of the filtered signal, where the __Dry Mix__ determines the amplitude of the unfiltered sound output.

Hard surfaces reflects the propagation of sound. For example a large canyon can be made more convincing with the Audio Echo Filter.

Sound propagates slower than light - we all know that from lightning and thunder. To simulate this, add an Audio Echo Filter to an event sound, set the Wet Mix to 0.0 and modulate the Delay to the distance between [AudioSource](class-AudioSource) and [AudioListener](class-AudioListener).
