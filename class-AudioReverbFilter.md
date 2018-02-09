#Audio Reverb Filter

The __Audio Reverb Filter__ takes an [Audio Clip](class-AudioClip) and distorts it to create a custom reverb effect.



##Properties

![](../uploads/Main/AudioReverbFilter.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Reverb Preset__ |Custom reverb presets, select user to create your own customized reverbs.|
|__Dry Level__ |Mix level of dry signal in output in mB. Ranges from -10000.0 to 0.0. Default is 0.|
|__Room__ |Room effect level at low frequencies in mB. Ranges from -10000.0 to 0.0. Default is 0.0.|
|__Room HF__ |Room effect high-frequency level in mB. Ranges from -10000.0 to 0.0. Default is 0.0.|
|__Room LF__ |Room effect low-frequency level in mB. Ranges from -10000.0 to 0.0. Default is 0.0.|
|__Decay Time__ |Reverberation decay time at low-frequencies in seconds. Ranges from 0.1 to 20.0. Default is 1.0.|
|__Decay HFRatio__ |Decay HF Ratio : High-frequency to low-frequency decay time ratio. Ranges from 0.1 to 2.0. Default is 0.5.|
|__Reflections Level__ |Early reflections level relative to room effect in mB. Ranges from -10000.0 to 1000.0. Default is -10000.0.|
|__Reflections Delay__ |Early reflections delay time relative to room effect in mB. Ranges from -10000.0 to 2000.0. Default is 0.0.|
|__Reverb Level__ |Late reverberation level relative to room effect in mB. Ranges from -10000.0 to 2000.0. Default is 0.0.|
|__Reverb Delay__ |Late reverberation delay time relative to first reflection in seconds. Ranges from 0.0 to 0.1. Default is 0.04.|
|__HFReference__ |Reference high frequency in Hz. Ranges from 20.0 to 20000.0. Default is 5000.0.|
|__LFReference__ |Reference low-frequency in Hz. Ranges from 20.0 to 1000.0. Default is 250.0.|
|__Diffusion__ |Reverberation diffusion (echo density) in percent. Ranges from 0.0 to 100.0. Default is 100.0.|
|__Density__ |Reverberation density (modal density) in percent. Ranges from 0.0 to 100.0. Default is 100.0.|

**Note:** These values can only be modified if your __Reverb Preset__ is set to __User__, else these values will be grayed out and they will have default values for each preset.


