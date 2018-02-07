# Custom Data module

The Custom Data module allows you to define custom data formats in the Editor to be attached to particles. You can also set this in a script. See documentation on [Particle System vertex streams](PartSysVertexStreams) for more information on how to set custom data from a script and feed that data into your shaders. 

Data can be in the form of a __Vector__, with up to 4 [MinMaxCurve](ScriptRef:ParticleSystem.MinMaxCurve.html) components, or a __Color__, which is an HDR-enabled [MinMaxGradient](ScriptRef:ParticleSystem.MinMaxGradient.html). Use this data to drive custom logic in your scripts and Shaders.

The default labels for each curve/gradient can be customized by clicking on them and typing in a contextual name. When passing custom data to shaders, it is useful to know how that data is used inside the shader. For example, a curve may be used for custom alpha testing, or a gradient may be used to add a secondary color to particles. By editing the labels, it is simple to keep a record in the UI of the purpose of each custom data entry.

![](../uploads/Main/CustomDataModule.png)

* <span class="page-edit">2017-09-04  <!-- include IncludeTextAmendPageSomeEdit --></span>
*  <span class="page-history">Editable custom data labels added in Unity  [2017.2](https://docs.unity3d.com/2017.2/Documentation/Manual/30_search.html?q=newin20172) <span class="search-words">NewIn20172</span></span>