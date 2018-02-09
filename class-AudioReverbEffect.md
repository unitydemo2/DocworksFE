#Audio SFX Reverb Effect

The __SFX Reverb Effect__ takes the output of an [Audio Mixer](class-AudioMixer) group and distorts it to create a custom reverb effect.



##Properties

![](../uploads/Main/AudioSFXReverbEffect.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Dry Level__ |Mix level of dry signal in output in mB. Ranges from -10000.0 to 0.0. Default is 0 mB.|
|__Room__ |Room effect level at low frequencies in mB. Ranges from -10000.0 to 0.0. Default is -10000.0 mB.|
|__Room HF__ |Room effect high-frequency level in mB. Ranges from -10000.0 to 0.0. Default is 0.0 mB.|
|__Decay Time__ |Reverberation decay time at low-frequencies in seconds. Ranges from 0.1 to 20.0. Default is 1.0.|
|__Decay HF Ratio__ |Decay HF Ratio : High-frequency to low-frequency decay time ratio. Ranges from 0.1 to 2.0. Default is 0.5.|
|__Reflections__ |Early reflections level relative to room effect in mB. Ranges from -10000.0 to 1000.0. Default is -10000.0 mB.|
|__Reflect Delay__ |Early reflections delay time relative to room effect in mB. Ranges from -10000.0 to 2000.0. Default is 0.02.|
|__Reverb__ |Late reverberation level relative to room effect in mB. Ranges from -10000.0 to 2000.0. Default is 0.0 mB.|
|__Reverb Delay__ |Late reverberation delay time relative to first reflection in seconds. Ranges from 0.0 to 0.1. Default is 0.04 s.|
|__Diffusion__ |Reverberation diffusion (echo density) in percent. Ranges from 0.0 to 100.0. Default is 100.0%.|
|__Density__ |Reverberation density (modal density) in percent. Ranges from 0.0 to 100.0. Default is 100.0%.|
|__HFReference__ |Reference high frequency in Hz. Ranges from 20.0 to 20000.0. Default is 5000.0 Hz.|
|__Room LF__ |Room effect low-frequency level in mB. Ranges from -10000.0 to 0.0. Default is 0.0 mB.|
|__LFReference__ |Reference low-frequency in Hz. Ranges from 20.0 to 1000.0. Default is 250.0 Hz.|

