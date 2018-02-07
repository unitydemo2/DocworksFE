#Limit Velocity Over Lifetime module

This module controls how the speed of particles is reduced over their lifetime.

![](../uploads/Main/PartSysLimVelLifeInsp.png)


##Properties

|**Property** |**Function** |
|:---|:---|
| __Separate Axes__ | Splits the axes up into separate X, Y and Z components. |
|__Speed__ |Sets the speed limit of the particles. |
|__Space__ |Selects whether the speed limitation refers to local or world space. This option is only available when __Separate Axes__ is enabled. |
|__Dampen__ |The fraction by which a particle's speed is reduced when it exceeds the speed limit. |
|__Drag__ |Applies linear drag to the particle velocities. |
|__Multiply by Size__ |When enabled, larger particles are affected more by the drag coefficient. |
|__Multiply by Velocity__ |When enabled, faster particles are affected more by the drag coefficient. |


##Details

This module is very useful for simulating air resistance that slows the particles, especially when a decreasing curve is used to lower the speed limit over time. For example, an explosion or firework initially bursts at great speed but the particles emitted from it rapidly slow down as they pass through the air.

The __Drag__ option offers a more physically accurate simulation of air resistance by offering options to apply varying amounts of resistance based on the size and speed of the particles.

---

*  <span class="page-edit">2017-09-05  <!-- include IncludeTextAmendPageYesEdit --></span>

*  <span class="page-history">Drag, Multiple by Size, Multiply by Velocity added in Unity [2017.2](https://docs.unity3d.com/2017.2/Documentation/Manual/30_search.html?q=newin20172)<span class="search-words">NewIn20172</span></span>