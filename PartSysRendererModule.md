# Renderer module

The Renderer module’s settings determine how a particle’s image or [Mesh](class-Mesh) is transformed, shaded and overdrawn by other particles.

![](../uploads/Main/PartSysRendererModule-0.png)

## Properties

| **Property**| **Function** |
|:---|:---| 
| __Render Mode__| How the rendered image is produced from the graphic image (or Mesh). See [Details](#Details), below, for more information. |
|&nbsp;&nbsp;&nbsp;&nbsp;Billboard| The particle always faces the Camera. |
|&nbsp;&nbsp;&nbsp;&nbsp;Stretched Billboard| The particle faces the Camera but with various scaling applied (see below). |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Camera Scale| Stretches particles according to Camera movement. Set this to 0 to disable Camera movement stretching. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Velocity Scale| Stretches particles proportionally to their speed. Set this to 0 to disable stretching based on speed. |
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Length Scale| Stretches particles proportionally to their current size along the direction of their velocity. Setting this to 0 makes the particles disappear, having effectively 0 length. |
|&nbsp;&nbsp;&nbsp;&nbsp;Horizontal Billboard| The particle plane is parallel to the XZ "floor" plane. |
|&nbsp;&nbsp;&nbsp;&nbsp;Vertical Billboard| The particle is upright on the world Y-axis, but turns to face the Camera. |
|&nbsp;&nbsp;&nbsp;&nbsp;Mesh| The particle is rendered from a 3D Mesh instead of a Texture. |
|&nbsp;&nbsp;&nbsp;&nbsp;None| This can be useful when using the [Trails](PartSysTrailsModule) module, if you want to only render the trails and hide the default rendering. |
| __Normal Direction__| Bias of lighting normals used for the particle graphics. A value of 1.0 points the normals at the Camera, while a value of 0.0 points them towards the center of the screen (Billboard modes only). |
| __Material__| Material used to render the particles. |
| __Trail Material__| Material used to render particle trails. This option is only available when the __Trails__ module is enabled. |
| __Sort Mode__| The order in which particles are drawn (and therefore overlaid). The possible values are __By Distance (from the Camera__), __Oldest in Front__, and __Youngest in Front__. Each particle within a system will be sorted according to this setting. |
| __Sorting Fudge__| Bias of particle system sort ordering. Lower values increase the relative chance that particle systems are drawn over other transparent GameObjects, including other particle systems. This setting only affects where an entire system appears in the scene - it does not perform sorting on individual particles within a system. |
| __Min Particle Size__| The smallest particle size (regardless of other settings), expressed as a fraction of viewport size. Note that this setting is only applied when the __Rendering Mode__ is set to __Billboard__. |
| __Max Particle Size__| The largest particle size (regardless of other settings), expressed as a fraction of viewport size. Note that this setting is only applied when the __Rendering Mode__ is set to __Billboard__. |
| __Billboard Alignment__| Use the drop-down to choose which direction particle billboards face. |
|&nbsp;&nbsp;&nbsp;&nbsp;View| Particles face the Camera plane. |
|&nbsp;&nbsp;&nbsp;&nbsp;World| Particles are aligned with the world axes. |
|&nbsp;&nbsp;&nbsp;&nbsp;Local| Particles are aligned to the Transform component of their GameObject.|
|&nbsp;&nbsp;&nbsp;&nbsp;Facing| Particles face the direct position of the Camera GameObject. |
| __Pivot__| Modify the pivot point used as the center for rotating particles. |
| __Visualize Pivot__| Preview the particle pivot points in the Scene View. |
| __Custom Vertex Streams__| Configure which particle properties are available in the Vertex Shader of your Material. See Particle System Vertex Streams for more details. |
| __Cast Shadows__| If enabled, the particle system creates shadows when a shadow-casting Light shines on it. |
|&nbsp;&nbsp;&nbsp;&nbsp;On| Select __On__ to enable shadows.  |
|&nbsp;&nbsp;&nbsp;&nbsp;Off| Select __Off__ to disable shadows. |
|&nbsp;&nbsp;&nbsp;&nbsp;Two-Sided| Select __Two Sided__ to allow shadows to be cast from either side of the Mesh (meaning backface culling is not taken into account). |
|&nbsp;&nbsp;&nbsp;&nbsp;Shadows Only| Select __Shadows Only__ to make it so that the shadows are visible, but the Mesh itself is not. |
| __Receive Shadows__| Dictates whether shadows can be cast onto particles. Only opaque materials can receive shadows. |
| __Sorting Layer__| Name of the Renderer’s sorting layer. |
| __Order in Layer__| This Renderer’s order within a sorting layer. |
| __Light Probes__| Probe-based lighting interpolation mode. |
| __Reflection Probes__| If enabled and reflection probes are present in the Scene, a reflection texture is picked for this GameObject and set as a built-in Shader uniform variable. |
| __Anchor Override__| A Transform used to determine the interpolation position when the [Light Probe](LightProbes) or [Reflection Probe](ReflectionProbes) systems are used. |

<a name="Details"> </a>
## Details

The __Render Mode__ lets you choose between several 2D Billboard graphic modes and Mesh mode. Using 3D Meshes gives particles extra authenticity when they represent solid GameObjects, such as rocks, and can also improve the sense of volume for clouds, fireballs and liquids. When 2D billboard graphics are used, the different options can be used for a variety of effects.

1. __Billboard mode__ is good for particles representing volumes that look much the same from any direction (such as clouds).

2. __Horizontal Billboard__ mode can be used when the particles cover the ground (such as target indicators and magic spell effects) or when they are flat objects that fly or float parallel to the ground (for example, shurikens).

3. __Vertical Billboard__ mode keeps each particle upright and perpendicular to the XZ plane, but allows it to rotate around its y-axis. This can be helpful when you are using an orthographic Camera and want particle sizes to stay consistent.

4. __Stretched Billboard__ mode accentuates the apparent speed of particles in a similar way to the "stretch and squash" techniques used by traditional animators. Note that in Stretched Billboard mode, particles are aligned to face the Camera and also aligned to their velocity. This alignment occurs regardless of the Velocity Scale value - even if Velocity Scale is set to 0, particles in this mode still align to the velocity.

The Normal Direction can be used to create spherical shading on the flat rectangular billboards. This can help create the illusion of 3D particles if you are using a Material that applies lighting to your particles. This setting is only used with the Billboard render modes.

