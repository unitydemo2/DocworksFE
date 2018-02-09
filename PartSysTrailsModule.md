# Trails module

Add trails to a percentage of your particles using this module. This module shares a number of properties with the [Trail Renderer](class-TrailRenderer) component, but offers the ability to easily attach Trails to particles, and to inherit various properties from the particles. Trails can be useful for a variety of effects, such as bullets, smoke, and magic visuals.


![](../uploads/Main/PartSysTrailsModule.png)

## Properties

| Property| Function |
|:---|:---| 
| __Ratio__| A value between 0 and 1, describing the proportion of particles that have a Trail assigned to them. Trails are assigned randomly, so this value represents a probability. |
| __Lifetime__| The lifetime of each vertex in the Trail, expressed as a multiplier of the lifetime of the particle it belongs to. When each new vertex is added to the Trail, it disappears after it has been in existence longer than its total lifetime. |
| __Minimum Vertex Distance__| Define the distance a particle must travel before its Trail receives a new vertex. |
| __Texture Mode__| Choose whether the Texture applied to the Trail is stretched along its entire length, or if it repeats every N units of distance. The repeat rate is controlled based on the __Tiling__ parameters in the __Material__. |
| __World Space__| When enabled, Trail vertices do not move relative to the Particle System’s GameObject, even if using __Local Simulation Space__. Instead, the Trail vertices are dropped in the world, and ignore any movement of the Particle System. |
| __Die With Particles__| If enabled (the box is checked), Trails vanish instantly when their particles die. If not enabled (the box is unchecked) the remaining Trail expires naturally based on its own remaining lifetime. |
| __Size Affects Width__| If enabled (the box is checked), the Trail width is multiplied by the particle size. |
| __Size Affects Lifetime__| If enabled (the box is checked), the Trail lifetime is multiplied by the particle size. |
| __Inherit Particle Color__| If enabled (the box is checked), the Trail color is modulated by the particle color. |
| __Color Over Lifetime__| A curve to control the color of the entire Trail over the lifetime of the particle it is attached to. |
| __Width Over Trail__| A curve to control the width of the Trail over its length. |
| __Color Over Trail__| A curve to control the color of the Trail over its length. |
