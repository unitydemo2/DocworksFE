#Particle System Shape Module

This module defines the shape (the volume or surface) from which [particles](PartSysWhatIs) can be emitted, and the direction of the start velocity. The __Shape__ property defines the shape of the emission volume, and the rest of the module’s properties vary depending on the Shape you choose.

All shapes (except [Mesh](class-Mesh)) have properties that define their dimensions, such as the __Radius__ property. To edit these, drag the handles on the wireframe emitter shape in the Scene view. The choice of shape affects the region from which particles can be launched, but also the initial direction of the particles. For example, a __Sphere__ emits particles outward in all directions, a __Cone__ emits a diverging stream of particles, and a __Mesh__ emits particles in directions that are normal to the surface.

The section below details the properties for each __Shape__.

##Shapes in the Shape module

###Sphere, Hemisphere

![](../uploads/Main/ShapeModule.png)

Note: Sphere and Hemisphere have the same properties.

| __Property__| __Function__ |
|:---|:---| 
| __Shape__| The shape of the emission volume. |
|     Sphere| Uniform emission in all directions. |
|     Hemisphere| Uniform emission in all directions on one side of a plane. |
| __Radius__| The radius of the circular aspect of the shape. |
| __Radius Thickness__| A value of 0 will emit from the outer surface of the shape. A value of 1 will use the entire volume. Values in between will use a proportion of the volume. |
| __Position__| Apply an offset to the emitter shape used for spawning particles. |
| __Rotation__| Rotate the emitter shape used for spawning particles. |
| __Scale__| Change the size of the emitter shape used for spawning particles. |
| __Align to Direction__| Use this checkbox to orient particles based on their initial direction of travel. This can be useful if you want to simulate, for example, chunks of car paint flying off a car’s bodywork during a collision. If the orientation is not satisfactory, you can also override it by applying a __Start Rotation__ value in the __Main__ module. |
| __Randomize Direction__| Use a value 0–1, to blend particle directions towards a random direction. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction is completely random. |
| __Spherize Direction__| Use a value 0–1, to blend particle directions towards a spherical direction, where they travel outwards from the center of their [Transform](class-Transform). When this is set to 0, this setting has no effect. When it is set to 1, the particle direction points outwards from the center (behaving identically to when the Shape is set to Sphere). |
| __Randomize Position__| Move particles by a random amount, up to the specified value. When this is set to 0, this setting has no effect. Any other value will apply some randomness to the spawning positions of the particles. |



###Cone

![](../uploads/Main/ShapeModule1.png)

| __Property__| __Function__ |
|:---|:---| 
| __Shape__| The shape of the emission volume. |
|     Cone| Emission from the base or body of a cone. The particles diverge in proportion to their distance from the cone’s center line. |
| __Angle__| The angle of the cone at its point. An angle of 0 produces a cylinder while an angle of 90 gives a flat disc. |
| __Radius__| The radius of the circular aspect of the shape. |
| __Radius Thickness__| A value of 0 will emit from the outer surface of the shape. A value of 1 will use the entire volume. Values in between will use a proportion of the volume. |
| __Arc__| The angular portion of a full circle that forms the emitter’s shape. |
|     __Mode__| Define how particles are generated around the arc of the shape. When set to __Random__, Unity generates particles randomly around the arc. If using __Loop__, particles are generated sequentially around the arc of the shape, and loops back to the start at the end of each cycle. __Ping-Pong__ is the same as __Loop__, except each consecutive loop happens in the opposite direction to the last. Finally, __Burst Spread__ mode distributes particle generation evenly around the shape. This can be used to give you an even spread of particles, compared to the default randomized behavior, where particles may clump together unevenly. Burst Spread is best used with burst emissions. |
|     __Spread__| Control the discrete intervals around the arc where particles may be generated. For example, a value of 0 will allow particles to spawn anywhere around the arc, and a value of 0.1 will only spawn particles at 10% intervals around the shape. |
|     __Speed__| Set a value for the speed the emission position moves around the arc. Using the small black drop-down next to the value field, set this to __Constant__ for the value to always remain the same, or __Curve__ for the value to change over time. |
| __Length__| The length of the cone. This only applies when the __Emit from:__ property is set to __Volume__. |
| __Emit from:__| Selects the part of the cone to emit from: __Base__ or __Volume__. |
| __Position__| Apply an offset to the emitter shape used for spawning particles. |
| __Rotation__| Rotate the emitter shape used for spawning particles. |
| __Scale__| Change the size of the emitter shape used for spawning particles. |
| __Align to Direction__| Use this checkbox to orient particles based on their initial direction of travel. This can be useful if you want to simulate, for example, chunks of car paint flying off a car’s bodywork during a collision. If the orientation is not satisfactory, you can also override it by applying a Start Rotation value in the Main module. |
| __Randomize Direction__| Use a value 0–1, to blend particle directions towards a random direction. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction is completely random. |
| __Spherize Direction__| Use a value 0–1, to blend particle directions towards a spherical direction, where they travel outwards from the center of their Transform. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction points outwards from the center (behaving identically to when the Shape is set to Sphere). |
| __Randomize Position__| Move particles by a random amount, up to the specified value. When this is set to 0, this setting has no effect. Any other value will apply some randomness to the spawning positions of the particles. |



###Box

![](../uploads/Main/ShapeModule2.png)

| __Property__| __Function__ |
|:---|:---| 
| __Shape__| The shape of the emission volume. |
|     Box| Emission from the edge, surface, or body of a box shape. The particles move in the emitter object’s forward (Z) direction. |
| __Emit from:__| Select the part of the box to emit from: __Edge__, __Shell__, or __Volume__. |
| __Position__| Apply an offset to the emitter shape used for spawning particles. |
| __Rotation__| Rotate the emitter shape used for spawning particles. |
| __Scale__| Change the size of the emitter shape used for spawning particles. |
| __Align to Direction__| Use this checkbox to orient particles based on their initial direction of travel. This can be useful if you want to simulate, for example, chunks of car paint flying off a car’s bodywork during a collision. If the orientation is not satisfactory, you can also override it by applying a Start Rotation value in the Main module. |
| __Randomize Direction__| Use a value 0–1, to blend particle directions towards a random direction. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction is completely random. |
| __Spherize Direction__| Use a value 0–1, to blend particle directions towards a spherical direction, where they travel outwards from the center of their Transform. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction points outwards from the center (behaving identically to when the Shape is set to Sphere). |
| __Randomize Position__| Move particles by a random amount, up to the specified value. When this is set to 0, this setting has no effect. Any other value will apply some randomness to the spawning positions of the particles. |



###Mesh, MeshRenderer, SkinnedMeshRenderer

![](../uploads/Main/ShapeModule3.png)

Mesh, MeshRenderer and SkinnedMeshRenderer have the same properties.

| __Property__| __Function__ |
|:---|:---| 
| __Shape__| The shape of the emission volume. |
|     Mesh| Emission from any arbitrary Mesh shape supplied via the Inspector. |
|     MeshRenderer| Emission from a reference to a GameObject’s Mesh Renderer. |
|     SkinnedMeshRenderer| Emission from a reference to a GameObject’s Skinned Mesh Renderer. |
| __Emission drop-down__| Use this drop-down to select where particles are emitted from. Select Vertex for the particles to emit from the vertices, Edge for the particles to emit from the edges, or Triangle for the particles to emit from the triangles. This is set to Vertex by default. |
| __Mesh__| The Mesh that provides the emitter’s shape. |
| __Single Material__| Should the particles be emitted from a particular sub-Mesh (identified by the material index number). If enabled, a numeric field is shown allowing you to specify the material index number. |
| __Use Mesh Colors__| Use, or disregard, Mesh colors. |
| __Normal Offset__| Distance away from the surface of the Mesh to emit particles (in the direction of the surface normal) |
| __Position__| Apply an offset to the emitter shape used for spawning particles. |
| __Rotation__| Rotate the emitter shape used for spawning particles. |
| __Scale__| Change the size of the emitter shape used for spawning particles. |
| __Align to Direction__| Use this checkbox to orient particles based on their initial direction of travel. This can be useful if you want to simulate, for example, chunks of car paint flying off a car’s bodywork during a collision. If the orientation is not satisfactory, you can also override it by applying a Start Rotation value in the Main module. |
| __Randomize Direction__| Use a value 0–1, to blend particle directions towards a random direction. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction is completely random. |
| __Spherize Direction__| Use a value 0–1, to blend particle directions towards a spherical direction, where they travel outwards from the center of their Transform. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction points outwards from the center (behaving identically to when the Shape is set to Sphere). |
| __Randomize Position__| Move particles by a random amount, up to the specified value. When this is set to 0, this setting has no effect. Any other value will apply some randomness to the spawning positions of the particles. |



####Mesh details

It is possible to choose to emit only from a particular material (sub-Mesh) by using the Single Material checkbox, and to offset the emission position along the Mesh’s normals, by using the Normal Offset property. This option allows users to offset particles from the surface of a Mesh.

It is also possible to ignore the color of the Mesh, with the __Use Mesh Colors__ checkbox.

###Circle

![](../uploads/Main/ShapeModule4.png)

| __Property__| __Function__ |
|:---|:---| 
| __Shape__| The shape of the emission volume. |
|     Circle| Uniform emission from the center or edge of a circle. The particles move only in the plane of the circle. |
| __Radius__| The radius of the circular aspect of the shape. |
| __Radius Thickness__| A value of 0 will emit from the outer edge of the circle. A value of 1 will use the entire area. Values in between will use a proportion of the area. |
| __Arc__| The angular portion of a full circle that forms the emitter’s shape. |
|     __Mode__| Define how particles are generated around the arc of the shape. When set to __Random__, Unity generates particles randomly around the arc. If using __Loop__, particles are generated sequentially around the arc of the shape, and loops back to the start at the end of each cycle. __Ping-Pong__ is the same as __Loop__, except each consecutive loop happens in the opposite direction to the last. Finally, __Burst Spread__ mode distributes particle generation evenly around the shape. This can be used to give you an even spread of particles, compared to the default randomized behavior, where particles may clump together unevenly. Burst Spread is best used with burst emissions. |
|     __Spread__| Control the discrete intervals around the arc where particles may be generated. For example, a value of 0 will allow particles to spawn anywhere around the arc, and a value of 0.1 will only spawn particles at 10% intervals around the shape. |
|     __Speed__| Set a value for the speed the emission position moves around the arc. Using the small black drop-down next to the value field, set this to __Constant__ for the value to always remain the same, or __Curve__ for the value to change over time. |
| __Position__| Apply an offset to the emitter shape used for spawning particles. |
| __Rotation__| Rotate the emitter shape used for spawning particles. |
| __Scale__| Change the size of the emitter shape used for spawning particles. |
| __Align to Direction__| Use this checkbox to orient particles based on their initial direction of travel. This can be useful if you want to simulate, for example, chunks of car paint flying off a car’s bodywork during a collision. If the orientation is not satisfactory, you can also override it by applying a Start Rotation value in the Main module. |
| __Randomize Direction__| Use a value 0–1, to blend particle directions towards a random direction. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction is completely random. |
| __Spherize Direction__| Use a value 0–1, to blend particle directions towards a spherical direction, where they travel outwards from the center of their Transform. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction points outwards from the center (behaving identically to when the Shape is set to Sphere). |
| __Randomize Position__| Move particles by a random amount, up to the specified value. When this is set to 0, this setting has no effect. Any other value will apply some randomness to the spawning positions of the particles. |



###Edge

![](../uploads/Main/ShapeModule5.png)

| __Property__| __Function__ |
|:---|:---| 
| __Shape__| The shape of the emission volume. |
|     Edge| Emission from a line segment. The particles move in the emitter object’s upward (Y) direction. |
| __Radius__| The radius property is used to define the length of the edge. |
|     __Mode__| Define how particles are generated along the radius of the shape. When set to __Random__, Unity generates particles randomly along the radius. If using __Loop__, particles are generated sequentially along the radius of the shape, and loops back to the start at the end of each cycle. __Ping-Pong__ is the same as __Loop__, except each consecutive loop happens in the opposite direction to the last. Finally, __Burst Spread__ mode distributes particle generation evenly along the radius. This can be used to give you an even spread of particles, compared to the default randomized behavior, where particles may clump together unevenly. Burst Spread is best used with burst emissions. |
|     __Spread__| Control the discrete intervals along the radius where particles may be generated. For example, a value of 0 will allow particles to spawn anywhere along the radius, and a value of 0.1 will only spawn particles at 10% intervals along the radius. |
|     __Speed__| Set a value for the speed the emission position moves along the radius. Using the small black drop-down next to the value field, set this to __Constant__ for the value to always remain the same, or __Curve__ for the value to change over time. |
| __Position__| Apply an offset to the emitter shape used for spawning particles. |
| __Rotation__| Rotate the emitter shape used for spawning particles. |
| __Scale__| Change the size of the emitter shape used for spawning particles. |
| __Align to Direction__| Use this checkbox to orient particles based on their initial direction of travel. This can be useful if you want to simulate, for example, chunks of car paint flying off a car’s bodywork during a collision. If the orientation is not satisfactory, you can also override it by applying a __Start Rotation__ value in the Main module. |
| __Randomize Direction__| Use a value 0–1, to blend particle directions towards a random direction. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction is completely random. |
| __Spherize Direction__| Use a value 0–1, to blend particle directions towards a spherical direction, where they travel outwards from the center of their Transform. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction points outwards from the center (behaving identically to when the Shape is set to Sphere). |
| __Randomize Position__| Move particles by a random amount, up to the specified value. When this is set to 0, this setting has no effect. Any other value will apply some randomness to the spawning positions of the particles. |



###Donut

![](../uploads/Main/ShapeModule6.png)

| __Property__| Function |
|:---|:---| 
| __Shape__| The shape of the emission volume. |
|     Donut| Emission from a Torus. The particles move outwards from the ring of the Torus. |
| __Radius__| The radius of the main donut ring. |
| __Donus Radius__| The thickness of the outer donut ring. |
| __Radius Thickness__| A value of 0 will emit from the outer edge of the circle. A value of 1 will use the entire area. Values in between will use a proportion of the area. |
| __Arc__| The angular portion of a full circle that forms the emitter’s shape. |
|     Mode| Define how particles are generated around the arc of the shape. When set to __Random__, Unity generates particles randomly around the arc. If using __Loop__, particles are generated sequentially around the arc of the shape, and loops back to the start at the end of each cycle. __Ping-Pong__ is the same as __Loop__, except each consecutive loop happens in the opposite direction to the last. Finally, __Burst Spread__ mode distributes particle generation evenly around the shape. This can be used to give you an even spread of particles, compared to the default randomized behavior, where particles may clump together unevenly. Burst Spread is best used with burst emissions. |
|     Spread| Control the discrete intervals around the arc where particles may be generated. For example, a value of 0 will allow particles to spawn anywhere around the arc, and a value of 0.1 will only spawn particles at 10% intervals around the shape. |
|     Speed| Set a value for the speed the emission position moves around the arc. Using the small black drop-down next to the value field, set this to __Constant__ for the value to always remain the same, or __Curve__ for the value to change over time. |
| __Position__| Apply an offset to the emitter shape used for spawning particles. |
| __Rotation__| Rotate the emitter shape used for spawning particles. |
| __Scale__| Change the size of the emitter shape used for spawning particles. |
| __Align To Direction__| Use this checkbox to orient particles based on their initial direction of travel. This can be useful if you want to simulate, for example, chunks of car paint flying off a car’s bodywork during a collision. If the orientation is not satisfactory, you can also override it by applying a __Start Rotation__ value in the Main module. |
| __Randomize Direction__| Use a value 0–1, to blend particle directions towards a random direction. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction is completely random. |
| __Spherize Direction__| Use a value 0–1, to blend particle directions towards a spherical direction, where they travel outwards from the center of their Transform. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction points outwards from the center (behaving identically to when the Shape is set to Sphere). |
| __Randomise Position__| Move particles by a random amount, up to the specified value. When this is set to 0, this setting has no effect. Any other value will apply some randomness to the spawning positions of the particles. |

<br/>
<br/>

---
* <span class="page-edit">2017-05-30  <!-- include IncludeTextAmendPageNoEdit --></span>

* <span class="page-history">Functionality of Shape Module updated in Unity  [2017.1](../Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>


