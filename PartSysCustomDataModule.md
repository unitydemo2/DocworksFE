# Custom Data module

The Custom Data module allows you to define custom data formats in the Editor to be attached to particles. You can also set this in a script. See documentation on [Particle System vertex streams](PartSysVertexStreams) for more information on how to set custom data from a script and feed that data into your shaders. 

Data can be in the form of a __Vector__, with up to 4 [MinMaxCurve](ScriptRef:ParticleSystem.MinMaxCurve.html) components, or a __Color__, which is an HDR-enabled [MinMaxGradient](ScriptRef:ParticleSystem.MinMaxGradient.html). Use this data to drive custom logic in your scripts and Shaders.

![](../uploads/Main/CustomDataModule.png)
