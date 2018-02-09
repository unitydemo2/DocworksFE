#Audio High Pass Effect

The __Highpass Effect__ passes high frequencies of an AudioMixer group and cuts off signals with frequencies lower than the __Cutoff Frequency__.


##Properties

![](../uploads/Main/AudioHighPassEffect.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Cutoff freq__ |Highpass cutoff frequency in Hertz (range 10.0 to 22000.0, default = 5000.0).|
|__Resonance__ |Highpass resonance quality value (range 1.0 to 10.0, default = 1.0).|


##Details

The __Resonance__ (short for Highpass Resonance Quality Factor) determines how much the filter's self-resonance is dampened. Higher highpass resonance quality indicates a lower rate of energy loss, that is the oscillations die out more slowly.