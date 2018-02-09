#Audio Low Pass Effect

The __Audio Low Pass Effect__ passes low frequencies of an [AudioMixer](class-AudioMixer) group while removing frequencies higher than the __Cutoff Frequency__.


##Properties

![](../uploads/Main/AudioLowPassEffect.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Cutoff freq__ |Lowpass cutoff frequency in Hertz (range 10.0 to 22000.0, default = 5000.0).|
|__Resonance__ |Lowpass resonance quality value (range 1.0 to 10.0, default = 1.0).|


##Details

The __Resonance__ (short for Lowpass Resonance Quality Factor) determines how much the filter's self-resonance is dampened. Higher lowpass resonance quality indicates a lower rate of energy loss, that is the oscillations die out more slowly.

