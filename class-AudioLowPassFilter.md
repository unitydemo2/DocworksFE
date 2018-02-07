#Audio Low Pass Filter

The __Audio Low Pass Filter__ passes low frequencies of an [AudioSource](class-AudioSource) or all sound reaching an [AudioListener](class-AudioListener) while removing frequencies higher than the __Cutoff Frequency__.


##Properties

![](../uploads/Main/AudioLowPassFilter.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Cutoff Frequency__ |Lowpass cutoff frequency in Hertz (range 0.0 to 22000.0, default = 5000.0).|
|__Lowpass Resonance Q__ |Lowpass resonance quality value (range 1.0 to 10.0, default = 1.0).|


##Details

The __Lowpass Resonance Q__ (short for Lowpass Resonance Quality Factor) determines how much the filter's self-resonance is dampened. Higher lowpass resonance quality indicates a lower rate of energy loss, that is the oscillations die out more slowly.

The __Audio Low Pass Filter__ has a Rolloff curve associated with it, making it possible to set __Cutoff Frequency__ over distance between the AudioSource and the AudioListener.

Sounds propagates very differently given the environment. For example, to compliment a visual fog effect add a subtle low-pass to the Audio Listener. The high frequencies of a sound being emitted from behind a door will be filtered out by the door and so won't reach the listener. To simulate this, simply change the Cutoff Frequency when opening the door.
