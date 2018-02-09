#Shape module

This module defines the shape (the volume or surface) from which [particles](PartSysWhatIs) can be emitted, and the direction of the start velocity. The __Shape__ property defines the shape of the emission volume, and the rest of the module’s properties vary depending on the Shape you choose.  

All shapes (except [Mesh](class-Mesh)) have properties that define their dimensions, such as the __Radius__ property. To edit these, drag the handles on the wireframe emitter shape in the Scene view. The choice of shape affects the region from which particles can be launched, but also the initial direction of the particles. For example, a __Sphere__ emits particles outward in all directions, a __Cone__ emits a diverging stream of particles, and a __Mesh__ emits particles in directions that are normal to the surface.

The section below details the properties for each __Shape__.

## Shapes in the Shape module

### Sphere, Hemisphere

![](../uploads/Main/PartSysShapeModule-0.png)

Sphere and Hemisphere have the same properties.

| **Property**| **Function** |
|:---|:---| 
| __Shape__| The shape of the emission volume. |
|&nbsp;&nbsp;&nbsp;&nbsp;Sphere| Uniform emission in all directions. |
|&nbsp;&nbsp;&nbsp;&nbsp;Hemisphere| Uniform emission in all directions on one side of a plane. |
| __Radius__| The radius of the circular aspect of the shape. |
| __Emit from Shell__| Enable this to make particles be emitted from the outer surface rather than the inner volume of the shape. |
| __Align to Direction__| Use this checkbox to orient particles based on their initial direction of travel. This can be useful if you want to simulate, for example, chunks of car paint flying off a car’s bodywork during a collision. If the orientation is not satisfactory, you can also override it by applying a __Start Rotation__ value in the __Main__ module. |
| __Randomize Direction__| Use a value 0-1, to blend particle directions towards a random direction. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction is completely random. |
| __Spherize Direction__| Use a value 0-1, to blend particle directions towards a spherical direction, where they travel outwards from the center of their [Transform](class-Transform). When this is set to 0, this setting has no effect. When it is set to 1, the particle direction points outwards from the center (behaving identically to when the Shape is set to Sphere). |

### Cone

![](../uploads/Main/PartSysShapeModule-1.png)

| **Property**| **Function** |
|:---|:---| 
| __Shape__| The shape of the emission volume. |
|&nbsp;&nbsp;&nbsp;&nbsp;Cone| Emission from the base or body of a cone. The particles diverge in proportion to their distance from the cone’s center line. |
| __Angle__| The angle of the cone at its point. An angle of 0 produces a cylinder while an angle of 90 gives a flat disc. |
| __Radius__| The radius of the circular aspect of the shape. |
| __Arc Mode__ (Randomized Arc)| Arc Mode appears as a property called __Randomized Arc__ in the Inspector. To change the __Arc Mode__, click the small black drop-down toggle to the right-hand side, next to the __Spread__ value field. The __Arc Mode__ defines how particles are generated around the arc of the shape. Use the first value for Arc Mode to define how much of the arc is used for emissions, using a value between 0 and 360. Use the second value, __Spread__, to control how particles are distributed around the shape, using a value between 0 and 1. For example, a value of 0 allows particles to be generated anywhere around the shape, while a value of 0.1 only allows particles to be generated at 10% intervals around the shape.|
|&nbsp;&nbsp;&nbsp;&nbsp;Random| When the __Arc Mode__ is set to __Random__, the property name appears in the Inspector as Randomized Arc. Unity generates particles randomly around the arc of the shape. |
|&nbsp;&nbsp;&nbsp;&nbsp;Loop| When the __Arc Mode__ is set to __Loop__, the property name appears in the Inspector as __Looping Arc__. Unity generates particles sequentially around the arc of the shape, and loops back to the start at the end of each cycle. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arc Speed| Set a value for the speed the emission position moves around the radius. Using the small black drop-down next to the value field, set this to __Constant__ for the value to always remain the same, or __Curve__ for the value to change over time. |
|&nbsp;&nbsp;&nbsp;&nbsp;Ping-Pong| When the __Arc Mode__ is set to __Ping-Pong__, the property name appears in the Inspector as __Ping-Pong Arc__. Unity generates particles sequentially around the radius of the shape, similar to __Looping Arc__, but alternating between clockwise and counter-clockwise at the end of each cycle. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arc Speed| Set a value for the speed the emission position moves around the arc. Using the small black drop-down next to the value field, set this to __Constant__ for the value to always remain the same, or __Curve__ for the value to change over time. |
|&nbsp;&nbsp;&nbsp;&nbsp;Burst Spread| When the __Arc Mode__ is set to __Burst Spread__, the property name appears in the Inspector as __Distributed Arc__. Unity distributes particle generation evenly around the shape. This can be used to give you an even spread of particles, compared to the default randomized behavior, where particles may clump together unevenly. Burst Spread is best used with burst emissions. |
| __Length__| The length of the cone. This only applies when the __Emit from:__ property is set to __Volume__ or __Volume Shell__. |
| __Emit from:__| Selects the part of the cone to emit from: __Base__, __Volume__, __Base Shell__ or __Volume Shell__. |
| __Align to Direction__| Use this checkbox to orient particles based on their initial direction of travel. This can be useful if you want to simulate, for example, chunks of car paint flying off a car’s bodywork during a collision. If the orientation is not satisfactory, you can also override it by applying a Start Rotation value in the Main module. |
| __Randomize Direction__| Use a value 0-1, to blend particle directions towards a random direction. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction is completely random. |
| __Spherize Direction__| Use a value 0-1, to blend particle directions towards a spherical direction, where they travel outwards from the center of their Transform. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction points outwards from the center (behaving identically to when the Shape is set to Sphere). |



### Box

![](../uploads/Main/PartSysShapeModule-2.png)

| **Property**| **Function** |
|:---|:---| 
| __Shape__| The shape of the emission volume. |
|&nbsp;&nbsp;&nbsp;&nbsp;Box| Emission from the edge, surface, or body of a box shape. The particles move in the emitter object’s forward (Z) direction. |
| __Box X, Y, Z__| Width, height and depth of the box shape. |
| __Emit from:__| Select the part of the box to emit from: __Edge__, __Shell__, or __Volume__. |
| __Align to Direction__| Use this checkbox to orient particles based on their initial direction of travel. This can be useful if you want to simulate, for example, chunks of car paint flying off a car’s bodywork during a collision. If the orientation is not satisfactory, you can also override it by applying a Start Rotation value in the Main module. |
| __Randomize Direction__| Use a value 0-1, to blend particle directions towards a random direction. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction is completely random. |
| __Spherize Direction__| Use a value 0-1, to blend particle directions towards a spherical direction, where they travel outwards from the center of their Transform. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction points outwards from the center (behaving identically to when the Shape is set to Sphere). |

### Mesh, MeshRenderer, SkinnedMeshRenderer

![](../uploads/Main/PartSysShapeModule-3.png)

Mesh, MeshRenderer and SkinnedMeshRenderer have the same properties.

| **Property**| **Function** |
|:---|:---| 
| __Shape__| The shape of the emission volume. |
|&nbsp;&nbsp;&nbsp;&nbsp;Mesh| Emission from any arbitrary Mesh shape supplied via the Inspector. |
|&nbsp;&nbsp;&nbsp;&nbsp;MeshRenderer| Emission from a reference to a GameObject’s Mesh Renderer. |
|&nbsp;&nbsp;&nbsp;&nbsp;SkinnedMeshRenderer| Emission from a reference to a GameObject’s Skinned Mesh Renderer. |
| __Emission drop-down__| Use this drop-down to select where particles are emitted from. Select Vertex for the particles to emit from the vertices, Edge for the particles to emit from the edges, or Triangle for the particles to emit from the triangles. This is set to Vertex by default. |
| __Mesh__| The Mesh that provides the emitter’s shape. |
| __Single Material__| Should the particles be emitted from a particular sub-Mesh (identified by the material index number). If enabled, a numeric field is shown allowing you to specify the material index number. |
| __Use Mesh Colors__| Use, or disregard, Mesh colors. |
| __Normal Offset__| Distance away from the surface of the Mesh to emit particles (in the direction of the surface normal) |
| __Mesh Scale__| Use this value to adjust the size of the source Mesh, defined in the __Mesh__ field. |
| __Align to Direction__| Use this checkbox to orient particles based on their initial direction of travel. This can be useful if you want to simulate, for example, chunks of car paint flying off a car’s bodywork during a collision. If the orientation is not satisfactory, you can also override it by applying a Start Rotation value in the Main module. |
| __Randomize Direction__| Use a value 0-1, to blend particle directions towards a random direction. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction is completely random. |
| __Spherize Direction__| Use a value 0-1, to blend particle directions towards a spherical direction, where they travel outwards from the center of their Transform. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction points outwards from the center (behaving identically to when the Shape is set to Sphere). |

#### Mesh details

It is possible to choose to emit only from a particular material (sub-Mesh) by using the Single Material checkbox, and to offset the emission position along the Mesh’s normals, by using the Normal Offset property. This option allows users to offset particles from the surface of a Mesh.

It is also possible to ignore the color of the Mesh, with the __Use Mesh Colors__ checkbox.

### Circle

![](../uploads/Main/PartSysShapeModule-4.png)

| **Property**| **Function** |
|:---|:---| 
| __Shape__| The shape of the emission volume. |
|&nbsp;&nbsp;&nbsp;&nbsp;Circle| Uniform emission from the center of edge of a circle. The particles move only in the plane of the circle. |
| __Radius__ | The radius of the circular aspect of the shape. |
| __Arc Mode__ (Randomized Arc)| Arc Mode appears as a property called __Randomized Arc__ in the Inspector. To change the __Arc Mode__, click the small black drop-down toggle to the right-hand side, next to the __Spread__ value field. The __Arc Mode__ defines how particles are generated around the arc of the shape. Use the first value for __Arc Mode__ to define how much of the arc is used for emissions, using a value between 0 and 360. Use the second value, __Spread__, to control how particles are distributed around the shape, using a value between 0 and 1. For example, a value of 0 allows particles to be generated anywhere around the shape, while a value of 0.1 only allows particles to be generated at 10% intervals around the shape.|
|&nbsp;&nbsp;&nbsp;&nbsp;Random| When the __Arc Mode__ is set to __Random__, the property name appears in the Inspector as __Randomized Arc__. Unity generates particles randomly around the arc of the shape. |
|&nbsp;&nbsp;&nbsp;&nbsp;Loop| When the __Arc Mode__ is set to __Loop__, the property name appears in the Inspector as __Looping Arc__. Unity generates particles sequentially around the arc of the shape, and loops back to the start at the end of each cycle. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arc Speed| Set a value for the speed the emission position moves around the radius. Using the small black drop-down next to the value field, set this to __Constant__ for the value to always remain the same, or __Curve__ for the value to change over time. |
|&nbsp;&nbsp;&nbsp;&nbsp;Ping-Pong| When the __Arc Mode__ is set to __Ping-Pong__, the property name appears in the Inspector as __Ping-Pong Arc__. Unity generates particles sequentially around the radius of the shape, similar to __Looping Arc__, but alternating between clockwise and counter-clockwise at the end of each cycle. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arc Speed| Set a value for the speed the emission position moves around the arc. Using the small black drop-down next to the value field, set this to __Constant__ for the value to always remain the same, or __Curve__ for the value to change over time.|
|&nbsp;&nbsp;&nbsp;&nbsp;Burst Spread| When the __Arc Mode__ is set to __Burst Spread__, the property name appears in the Inspector as __Distributed Arc__. Unity distributes particle generation evenly around the shape. This can be used to give you an even spread of particles, compared to the default randomized behavior, where particles may clump together unevenly. <br/><br/>__Burst Spread__ is best used with burst emissions. |
| __Emit From Edge__| Enable this to make particles be emitted from the edge of the circle rather than the center. |
| __Align to Direction__| Use this checkbox to orient particles based on their initial direction of travel. This can be useful if you want to simulate, for example, chunks of car paint flying off a car’s bodywork during a collision. If the orientation is not satisfactory, you can also override it by applying a Start Rotation value in the Main module. |
| __Randomize Direction__| Use a value 0-1, to blend particle directions towards a random direction. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction is completely random. |
| __Spherize Direction__| Use a value 0-1, to blend particle directions towards a spherical direction, where they travel outwards from the center of their Transform. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction points outwards from the center (behaving identically to when the Shape is set to Sphere). |



### Edge

![](../uploads/Main/PartSysShapeModule-5.png)

| **Property**| **Function** |
|:---|:---| 
| __Shape__| The shape of the emission volume. |
|&nbsp;&nbsp;&nbsp;&nbsp;Edge| Emission from a line segment. The particles move in the emitter object’s upward (Y) direction. |
| __Radius Mode__ (Randomized Radius)| __Radius Mode__ appears as a property called __Randomized Radius__ in the Inspector. To change the __Radius Mode__, click the small black drop-down toggle to the right-hand side, next to the __Spread__ value field. The __Radius Mode__ defines how particles are generated around the radius of the shape. Use the first value for Radius Mode to define how much of the radius is used for emissions, using a value between 0 and 360. Use the second value, __Spread__, to control how particles are distributed around the shape, using a value between 0 and 1. For example, a value of 0 allows particles to be generated anywhere around the shape, while a value of 0.1 only allows particles to be generated at 10% intervals around the shape. |
|&nbsp;&nbsp;&nbsp;&nbsp;Random| When the __Radius Mode__ is set to __Random__, the property name appears in the Inspector as __Randomized Radius__. Unity generates particles randomly around the radius of the shape. |
|&nbsp;&nbsp;&nbsp;&nbsp;Loop| When the __Radius Mode__ is set to __Loop__, the property name appears in the Inspector as __Looping Radius__. Unity generates particles sequentially around the radius of the shape, and loops back to the start at the end of each cycle. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Radius Speed| Set a value for the speed the emission position moves around the radius. Using the small black drop-down next to the value field, set this to __Constant__ for the value to always remain the same, or __Curve__ for the value to change over time. |
|&nbsp;&nbsp;&nbsp;&nbsp;Ping-Pong| When the __Radius Mode__ is set to __Ping-Pong__, the property name appears in the Inspector as __Ping-Pong Radius__. Unity generates particles sequentially around the radius of the shape, similar to __Looping Radius__, but alternating between clockwise and counter-clockwise at the end of each cycle. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Radius Speed| Set a value for the speed the emission position moves around the radius. Using the small black drop-down next to the value field, set this to __Constant__ for the value to always remain the same, or __Curve__ for the value to change over time. |
|&nbsp;&nbsp;&nbsp;&nbsp;Burst Spread| When the Radius Mode is set to __Burst Spread__, the property name appears in the Inspector as __Distributed Radius__. Unity distributes particle generation evenly around the shape. Use this to give you an even spread of particles, compared to the default randomized behavior, where particles may clump together unevenly. __Burst Spread__ is best used with burst emissions. |
| __Align to Direction__| Use this checkbox to orient particles based on their initial direction of travel. This can be useful if you want to simulate, for example, chunks of car paint flying off a car’s bodywork during a collision. If the orientation is not satisfactory, you can also override it by applying a __Start Rotation__ value in the Main module. |
| __Randomize Direction__| Use a value 0-1, to blend particle directions towards a random direction. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction is completely random. |
| __Spherize Direction__| Use a value 0-1, to blend particle directions towards a spherical direction, where they travel outwards from the center of their Transform. When this is set to 0, this setting has no effect. When it is set to 1, the particle direction points outwards from the center (behaving identically to when the Shape is set to Sphere). |



