# Trails module

Add trails to a percentage of your particles using this module. This module shares a number of properties with the [Trail Renderer](class-TrailRenderer) component, but offers the ability to easily attach Trails to particles, and to inherit various properties from the particles. Trails can be useful for a variety of effects, such as bullets, smoke, and magic visuals.

![The Trails module in __Particles__ mode](../uploads/Main/PartSysTrailsModule.png)

![The Trails module in __Ribbon__ mode](../uploads/Main/PartSysTrailsModuleRibbon.png)

## Properties



|**Property:** |**Function:** |
|:---|:---|
|__Mode__| Choose how trails are generated for the Particle System. <br/>- __Particle__ mode creates an effect where each particle leaves a stationary trail in its path. <br/>- __Ribbon__ mode create a ribbon of trails connecting each particle based on its age. |
|__Ratio__| A value between 0 and 1, describing the proportion of particles that have a Trail assigned to them. Unity assigns trails randomly, so this value represents a probability. |
| __Lifetime__ | The lifetime of each vertex in the Trail, expressed as a multiplier of the lifetime of the particle it belongs to. When each new vertex is added to the Trail, it disappears after it has been in existence longer than its total lifetime. |
| __Minimum Vertex Distance__| Define the distance a particle must travel before its Trail receives a new vertex. |
| __World Space__| When enabled, Trail vertices do not move relative to the Particle System’s GameObject, even if using __Local Simulation Space__. Instead, the Trail vertices are dropped in the world, and ignore any movement of the Particle System. |
| __Die With Particles__| If this box is checked, Trails vanish instantly when their particles die. If this box is not checked, the remaining Trail expires naturally based on its own remaining lifetime. |
| __Ribbon Count__| Choose how many ribbons to render throughout the Particle System. A value of 1 creates a single ribbon connecting each particle. However, a value higher than 1 creates ribbons that connect every Nth particle. For example, when using a value of 2, there will be one ribbon connecting particles 1, 3, 5, and another ribbon connecting particles 2, 4, 6, and so on. The ordering of the particles is decided based on their age. |
| __Split Sub Emitter Ribbons__| When enabled on a system that is being used as a sub-emitter, particles that were spawned from the same parent system particle share a ribbon. | 
| __Texture Mode__| Choose whether the Texture applied to the Trail is stretched along its entire length, or if it repeats every N units of distance. The repeat rate is controlled based on the __Tiling__ parameters in the __Material__. | 
| __Size affects Width__| If enabled (the box is checked), the Trail width is multiplied by the particle size. |
| __Size affects Lifetime__| If enabled (the box is checked), the Trail lifetime is multiplied by the particle size.|
| __Inherit Particle Color__| If enabled (the box is checked), the Trail color is modulated by the particle color. |
| __Color over Lifetime__| A curve to control the color of the entire Trail over the lifetime of the particle it is attached to. |
| __Width over Trail__| A curve to control the width of the Trail over its length. |
| __Color over Trail__| A curve to control the color of the Trail over its length. |
| __Generate Lighting Data__| Enable this (check the box), to build the Trail geometry with Normals and Tangents included. This allows them to use Materials that use the scene lighting, for example via the Standard Shader, or by using a custom shader. |


<br/>

----
*  <span class="page-edit">2017-10-26  <!-- include IncludeTextAmendPageSomeEdit --></span>

*  <span class="page-history">__Size affects Width__, __Size affects Lifetime__, __Color over Lifetime__, __Width over Trail__, __Color over Trail__, and __Generate Lighting Data__ added in Unity [2017.1](../Manual/30_search.html?q=newin20171)<span class="search-words">NewIn20171</span></span>

*  <span class="page-history">__Particle__ mode added in Unity [2017.3](../Manual/30_search.html?q=newin20173)<span class="search-words">NewIn20173</span></span>
