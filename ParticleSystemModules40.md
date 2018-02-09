Particle System Modules (Shuriken)
==================================


The Particle System (Shuriken) uses modules to describe the behaviour of particles over time. The modules are documented in detail here. For an introduction to modules see [this page](ParticleSystemModulesIntro).


Initial Module
--------------


![](../uploads/Main/ShurikenInitialModule.png) 
This module is always present, it cannot be removed or disabled.

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Duration__ |The duration the Particle System will be emitting particles.|
|__Looping__ |Is the Particle System looping.|
|__Prewarm__ |Only looping systems can be prewarmed which means that the Particle System will have emitted particles at start as if it had already emitted particles one cycle. |
|__Start Delay__ |Delay in seconds that this Particle System will wait before emitting particles. Note prewarmed looping systems cannot use a start delay.|
|__Start Lifetime__ |The lifetime of particles in seconds (see [MinMaxCurve](ParticleSystemCurveEditor)). |
|__Start Speed__ |The speed of particles when emitted (see [MinMaxCurve](ParticleSystemCurveEditor)).|
|__Start Size__ |The size of particles when emitted (see [MinMaxCurve](ParticleSystemCurveEditor)).|
|__Start Rotation__ |The rotation of particles when emitted (see [MinMaxCurve](ParticleSystemCurveEditor)).|
|__Randomize Rotation Direction__ |Configure a percentage of spawned particles to spin in the opposite direction.|
|__Start Color__ |The color of particles when emitted (see [MinMaxGradient](ParticleSystemColorEditor)).|
|__Gravity Modifier__ |The amount of gravity that will affect particles during their lifetime.|
|__Inherit Velocity__ |Factor for controlling the amount of velocity the particles should inherit of the transform of the Particle System (for moving Particle Systems).|
|__Simulation Space__ |Simulate the Particle System in local space or world space.|
|__Play On Awake__ |If enabled the Particle System will automatically start when it's created.|
|__Max Particles__ |Max number of particles the Particle System will emit.|



Emission Module
---------------


![](../uploads/Main/ShurikenEmissionModule.png) 
Controls the rate of particles being emitted and allows spawning large groups of particles at certain moments (over Particle System duration time). Useful for explosions when a bunch of particles need to be created at once.

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Rate__ |Amount of particles emitted over Time (per second) or Distance (per meter) (see [MinMaxCurve](ParticleSystemCurveEditor)).|
|__Bursts__ (Time option only) |Add bursts of particles that occur within the duration of the Particle System.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Time and Number of Particles__ |Specify time (in seconds within duration) that a specified amount of particles should be emitted. Use the + and - for adjusting number of bursts.|

Shape Module
------------


![](../uploads/Main/ShurikenShapeModule.png) 
Defines the shape of the emitter: Sphere, Hemisphere, Cone, Box and Mesh. Can apply initial force along the surface normal or random direction.


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Sphere__ | |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Radius__ |Radius of the sphere. (Can also be manipulated by handles in the Scene View).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Emit from Shell__ |Emit from shell of the sphere. If disabled, particles will be emitted from the volume of the sphere.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Random Direction__|Should particles have a random direction when emitted or a direction along the surface normal of the sphere?|
|__Hemisphere__ | |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Radius__ |Radius of the hemisphere. (Can also be manipulated by handles in the Scene View).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Emit from Shell__ |Emit from shell of the hemisphere. If disabled particles will be emitted from the volume of the hemisphere.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Random Direction__|Should particles have a random direction when emitted or a direction along the surface normal of the hemisphere?|
|__Cone__ | |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Angle__ |Angle of the cone. If angle is 0 then particles will be emitted in one direction. (Can also be manipulated by handles in the Scene View).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Radius__ |The radius at the point of emission. If the value is near zero emission will be from a point. A larger value basically creates a capped cone, emission coming from a disc rather than a point. (Can also be manipulated by handles in the Scene View).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Length__ |Length of the emission volume. Only available when emitting from a Volume or Volume Shell. (Can also be manipulated by handles in the Scene View).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Emit From__ |Determines where emission originates from. Possible values are Base, Base Shell, Volume and Volume Shell.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Random Direction__|Should particles have a random direction when emitted or a direction along the cone?|
|__Box__ | |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Box X__ |Scale of box in X. (Can also be manipulated by handles in the Scene View).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Box Y__ |Scale of box in Y. (Can also be manipulated by handles in the Scene View).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Box Z__ |Scale of box in Z. (Can also be manipulated by handles in the Scene View).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Random Direction__|Should particles have a random direction when emitted or a direction along the Z-axis of the box?|
|__Mesh__ | |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Type__ |Particles can be emitted from either Vertex, Edge or Triangle.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Mesh__ |Select Mesh that should be used as emission shape.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Random Direction__|Should particles have a random direction when emitted or a direction along the surface of the mesh?|
|__Circle__ | |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Radius__ |Radius of the circle. (Can also be manipulated by the square handles in the Scene View).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Arc__ |Angle of the arc. (Can also be manipulated by the circular handle in the Scene View).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Emit from Edge__ |Emit from edge of the circle. If disabled, particles will be emitted from the area of the circle.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Random Direction__|Should particles have a random direction when emitted or a direction along the surface normal of the circle?|
|__Edge__ | |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Radius__ |Half length of the edge. (Can also be manipulated by the square handles in the Scene View).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Random Direction__|Should particles have a random direction when emitted or go straight up (Y axis)?|

Velocity Over Lifetime Module
-----------------------------


![](../uploads/Main/ShurikenVelocityOverLifetimeModule.png) 
Directly animates velocity of the particle. Mostly useful for particles which has complex physical, but simple visual behavior (like smoke with turbulence and temperature loss) and has little interaction with physical world.

|**_Property:_** |**_Function:_** |
|:---|:---|
|__XYZ__ |Use either constant values for curves or random between curves for controlling the movement of the particles. See [MinMaxCurve](ParticleSystemCurveEditor).|
|__Space__ |Local / World: Are the velocity values in local space or world space? |


Limit Velocity Over Lifetime Module
-----------------------------------


![](../uploads/Main/ShurikenLimitVelocityOverLifetimeModule.png) 
Basically can be used to simulate drag. Dampens or clamps velocity, if it is over certain threshold. Can be configured per axis or per vector length.

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Separate Axis__ |Use for setting per axis control.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Speed__ |Specify magnitude as constant or by curve that will limit all axes of velocity. See [MinMaxCurve](ParticleSystemCurveEditor).|
|__Dampen__ |(0-1) value that controls how much the exceeding velocity should be dampened. For example, a value of 0.5 will dampen exceeding velocity by 50%.|


Force Over Lifetime Module
--------------------------


![](../uploads/Main/ShurikenForceOverLifetimeModule.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__XYZ__ |Use either constant values for curves or random between curves for controlling the force applied to the particles. See [MinMaxCurve](ParticleSystemCurveEditor).|
|__Space__ |Local / World: Are the velocity values in local space or world space |
|__Randomize__ |Randomize the force applied to the particles every frame. |

Color Over Lifetime Module
--------------------------


![](../uploads/Main/ShurikenColorOverLifetimeModule.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Color__ |Controls the color of each particle during its lifetime. If some particles have a shorter lifetime than others, they will animate faster. Use constant color, random between two colors, animate it using gradient or specify a random color using two gradients (see [Gradient](GradientEditor)). Note that this colour will be _multiplied_ by the value in the __Start Color__ property - if the Start Color is black then Color Over Lifetime will not affect the particle.|

Color By Speed Module
---------------------


![](../uploads/Main/ShurikenColorBySpeedModule.png) 
Animates particle color based on its speed. Remaps speed in the defined range to a color.

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Color__ |Color used for remapping of speed. Use gradients for varying colors. See [MinMaxGradient](ParticleSystemColorEditor).|
|__Speed Range__ |The min and max values for defining the speed range which is used for remapping a speed to a color.|


Size Over Lifetime Module
-------------------------


![](../uploads/Main/ShurikenSizeOverLifetimeModule.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Size__ |Controls the size of each particle during its lifetime. Use constant size, animate it using a curve or specify a random size using two curves. See [MinMaxCurve](ParticleSystemCurveEditor).|

Size By Speed Module
--------------------


![](../uploads/Main/ShurikenSizeBySpeedModule.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Size__ |Size used for remapping of speed. Use curves for varying sizes. See [MinMaxCurve](ParticleSystemCurveEditor).|
|__Speed Range__ |The min and max values for defining the speed range which is used for remapping a speed to a size.|


Rotation Over Lifetime Module
-----------------------------


![](../uploads/Main/ShurikenRotationOverLifetime.png) 
Specify values in degrees.

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Angular Velocity__ |Controls the rotational speed of each particle during its lifetime. Use constant rotational speed, animate it using a curve or specify a random rotational speed using two curves. See [MinMaxCurve](ParticleSystemCurveEditor).|


Rotation By Speed Module
------------------------


![](../uploads/Main/ShurikenRotationBySpeedModule.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Angular Velocity__ |Rotational speed used for remapping of a particle's speed. Use curves for varying rotational speeds. See [MinMaxCurve](ParticleSystemCurveEditor).|
|__Speed Range__ |The min and max values for defining the speed range which is used for remapping a speed to a rotational speed.|


External Forces Module
----------------------


![](../uploads/Main/ShurikenExtForcesModule.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Multiplier__|Scale factor that determines how much the particles are affected by wind zones (i.e., the wind force vector is multiplied by this value).|


Collision Module
----------------


![](../uploads/Main/ShurikenCollisionModule40.png) 
Set up collisions for the particles of this Particle System. World and planar collisions are supported. Planar collision is very efficient for simple collision detection. Planes are set up by referencing an existing transform in the scene or by creating a new empty GameObject for this purpose. Another benefit of planar collision is that particle systems with collision planes can be set up as prefabs. World collision uses raycasts so must be used with care in order to ensure good performance. However, for cases where approximate collisions are acceptable world collision in __Low__ or __Medium__ quality can be very efficient.

###Properties common for any Collision Module

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Planes/World__ |Specify the collision type: __Planes__ for planar collision or __World__ for world collisions.|
|__Dampen__ |(0-1) When the particle collides, it will keep this fraction of its speed. Unless it is set to 1.0, the particle will become slower after collision.|
|__Bounce__ |(0-1) When the particle collides, it will keep this fraction of the component of the velocity, which is normal to the plane of collision.|
|__Lifetime Loss__ |(0-1) The fraction of Start Lifetime lost on each collision. When lifetime reaches 0, the particle dies. For example if a particle should die on first collision, set this to 1.0.|
|__Min Kill Speed__ |The minimum speed of a particle before it is killed.|
|__Send Collision Messages__ |Whether to send collision messages and thus trigger [OnParticleCollision](ScriptRef:MonoBehaviour.OnParticleCollision.html) callbacks on GameObjects and ParticleSystems.|

###Properties available only in the __Planes__ Mode

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Planes__ |Planes are defined by assigning a reference to a transform. This transform can be any transform in the scene and can be animated. Multiple planes can be used. Note: the Y-axis is used as the normal of a plane.|
|__Visualization__ |Only used for visualizing the planes: Grid or Solid.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Grid__ |Rendered as gizmos and is useful for quick indication of position and orientation in the world.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Solid__ |Renders a plane in the scene which is useful for exact positioning of a plane.|
|__Scale Plane__ |Resizes the visualization planes.|
|__Particle Radius__ |The assumed radius of the particle for collision purposes. (So particles are treated as spheres.)|


###Properties available only in the __World__ Mode

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Collides With__ |Filter for specifying colliders. Select __Everything__ to colllide with the whole world.|
|__Collision Quality__|The quality of the world collision.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__High__ |All particles performs a scene raycast per frame. Note: This is CPU intensive, it should only be used with 1000 simultaneous particles (scene wide) or less.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Medium__ |The particle system receives a share of the globally set __Particle Raycast Budget__ (see [Particle Raycast Budget](class-QualitySettings)) in each frame. Particles are updated in a round-robin fashion where particles that do not receive a raycast in a given frame will lookup and use older collisions stored in a cache. Note: This collision type is approximate and some particles will leak, particularly at corners.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Low__ |Same as __Medium__ except the particle system is only awarded a share of the __Particle Raycast Budget__ every fourth frame.|
|__Voxel Size__ |Density of the voxels used for caching intersections used in the __Medium__ and __Low__ quality setting. The size of a voxel is given in scene units. Usually, 0.5 - 1.0 should be used (assuming metric units).|


Sub Emitter Module
------------------


![](../uploads/Main/ShurikenSubEmitter.png) 
This is a powerful module that enables spawning of other Particle Systems at the follwing particle events: birth, death or collision of a particle.

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Birth__ |Spawn another Particle System at birth of each particle in this Particle System.|
|__Death__ |Spawn another Particle System at death of each particle in this Particle System.|
|__Collision__ |Spawn another Particle System at collision of each particle in this Particle System. IMPORTANT: Collision needs to be set up using the Collision Module. See Collision Module.|

Texture Sheet Animation Module
------------------------------


![](../uploads/Main/ShurikenTextureSheetModule.png) 
Animates UV coordinates of the particle over its lifetime. Animation frames can be presented in a form of a grid or every row in the sheet can be separate animation. The frames are animated with curves or can be a random frame between two curves. The speed of the animation is defined by "Cycles".
IMPORTANT: The texture used for animation is the one used by the material found in the Renderer module.

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Tiles__ |Define the tiling of the texture.|
|__Animation__ |Specify the animation type: Whole Sheet or Single Row.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Whole Sheet__ |Uses the whole sheet for uv animation.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__- Frame over Time__ |Controls the uv animation frame of each particle during its lifetime over the whole sheet. Use constant, animate it using a curve or specify a random frame using two curves. See [MinMaxCurve](ParticleSystemCurveEditor).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Single Row__ |Uses a single row of the texture sheet for uv animation.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__- Random Row__ |If checked, the start row will be random, and if unchecked, the row index can be specified (first row is 0).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__- Frame over Time__ |Controls the uv animation frame of each particle during its lifetime within the specified row. Use constant, animate it using a curve or specify a random frame using two curves. See [MinMaxCurve](ParticleSystemCurveEditor).|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__- Cycles__ |Specify speed of animation.|


Renderer Module
---------------


![](../uploads/Main/ShurikenRendererModule40.png) 
The renderer module exposes the __ParticleSystemRenderer__ component's properties. Note that even though a GameObject has a __ParticleSystemRenderer__ component, its properties are only exposed here. When this module is removed/added, it is actually the __ParticleSystemRenderer__ component that is added or removed.


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Render Mode__ |Select one of the following particle render modes.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Billboard__ |Makes the particles always face the camera.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Stretched Billboard__ |Particles are stretched using the following parameters.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__- Camera Scale__ |How much the camera speed is factored in when determining particle stretching.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__- Speed Scale__ |Defines the length of the particle compared to its speed.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__- Length Scale__ |Defines the length of the particle compared to its width.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Horizontal Billboard__ |Makes the particles align with the XZ plane. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Vertical Billboard__ |Makes the particles align with the Y axis while facing the camera.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Mesh__ |Particles are rendered using a mesh instead of a quad.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__- Mesh__ |The reference to the mesh used for rendering particles.|
|__Normal Direction__ |Value from 0 to 1 that determines how much normals point toward the camera (0) and how much sideways toward the centre of the view (1).|
|__Material__ |Material used by billboarded or mesh particles.|
|__Sort Mode__ |The draw order of particles can be sorted by distance, youngest first, or oldest first.|
|__Sorting Fudge__ |Use this to affect the draw order. Particle systems with _lower_ sorting fudge numbers are more likely to be drawn last, and thus appear in front of other transparent objects, including other particles.|
|__Cast Shadows__ |Should particles cast shadows? May or may not be possible depending on the material.|
|__Receive Shadows__ |Should particles receive shadows? May or may not be possible depending on the material.|
|__Max Particle Size__ |Set max relative viewport size. Valid values: 0-1. |
