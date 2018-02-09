#Audio Low Pass Simple Effect

The __Audio Low Pass Simple Effect__ passes low frequencies of an [AudioMixer](class-AudioMixer) group while removing frequencies higher than the __Cutoff Frequency__.


##Properties

![](../uploads/Main/AudioLowPassSimpleEffect.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Cutoff freq__ |Lowpass cutoff frequency in Hertz (range 10.0 to 22000.0, default = 5000.0).|


##Details

The __Resonance__ (short for Lowpass Resonance Quality Factor) determines how much the filter's self-resonance is dampened. Higher lowpass resonance quality indicates a lower rate of energy loss, that is the oscillations die out more slowly.

For additional control over the resonance value of the low pass filter use the [Audio Low Pass effect](class-AudioLowPassEffect).