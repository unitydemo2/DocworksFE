#Limit Velocity Over Lifetime module

This module controls how the speed of particles is reduced over their lifetime.

![](../uploads/Main/PartSysLimVelLifeInsp.png)

##Properties

|**Property** |**Function** |
|:---|:---|
| __Separate Axes__ | Splits the axes up into separate X, Y and Z components. |
|__Speed__ |Set the speed limit of the particles. |
|__Space__ |Selects whether the speed limitation refers to local or world space. This option is only available when __Separate Axes__ is enabled. |
|__Dampen__ |The fraction by which a particle's speed is reduced when it exceeds the speed limit. |

##Details

This effect is very useful for simulating air resistance that slows the particles, especially when a decreasing curve is used to lower the speed limit over time. For example, an explosion or firework initially bursts at great speed but the particles emitted from it rapidly slow down as they pass through the air.