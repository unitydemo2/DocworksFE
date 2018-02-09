Particle Effects (Shuriken)
===========================


An important feature of Unity's Particle System is that individual Particle Systems can be grouped by being parented to the same root. We will use the term __Paricle Effect__ for such a group. Particle Systems belonging to the same Particle Effect, are played, stopped and paused together.

For managing complex particle effects, Unity provides a Particle Editor, which can be accessed from the [Inspector](ParticleSystemInspector), by pressing __Open Editor__ 

![Overview of the Particle System Editor](../uploads/Main/ShurikenParticleEditor.png) 

You can toggle between __Show: All__ and __Show: Selected__ in this Editor. __Show: All__ will render the entire particle effect. __Show: Selected__ will only render the selected particle systems. What is selected will be highlighted with a blue frame in the Particle Editor and also shown in blue in the Hierarchy view. You can also change the selection both from the Hierarchy View and the Particle Editor, by clicking the icon in the top-left corner of the Particle System. To do a multiselect, use Ctrl+click on windows and Command+click on the Mac. 

You can explicitly control rendering order of grouped particles (or otherwise spatially close particle emitters) by tweaking __Sorting Fudge__ property in the [__Renderer__ module](ParticleSystemModules40#RendererModule). 



![](../uploads/Main/ShurikenOverviewHierarchy.png) 

_Particle Systems in the same hierarchy are considered as part of the same Particle Effect. This hierarchy shows the setup of the effect shown above._
