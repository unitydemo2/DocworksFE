#Audio Echo Effect

The __Audio Echo Effect__ repeats a sound after a given __Delay__, attenuating the repetitions based on the __Decay Ratio__.


##Properties

![](../uploads/Main/AudioEchoEffect.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Delay__ |Echo delay in ms. 10 to 5000. Default = 500.|
|__Decay__ |Echo decay per delay. 0 to 100%. 100% = No decay, 0% = total decay (ie simple 1 line delay). Default = 50%.|
|__Max channels__ ||
|__Drymix__ |Volume of original signal to pass to output. 0 to 100%. Default = 100%.|
|__Wetmix__ |Volume of echo signal to pass to output. 0 to 100%. Default = 100%.|



##Details

The __Wetmix__ value determines the amplitude of the filtered signal, where the __Drymix__ determines the amplitude of the unfiltered sound output.

Hard surfaces reflects the propagation of sound. For example a large canyon can be made more convincing with the Audio Echo Filter.

