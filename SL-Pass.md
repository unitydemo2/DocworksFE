#ShaderLab: Pass

The Pass block causes the geometry of a GameObject to be rendered once.


##Syntax

````
Pass { [Name and Tags] [RenderSetup] }
````

The basic Pass command contains a list of render state setup commands.


##Name and tags

A Pass can define its [Name](SL-Name) and arbitrary number of [Tags](SL-PassTags). These are name/value strings that communicate the Pass's intent to the rendering engine.

##Render state set-up

A Pass sets up various states of the graphics hardware, such as whether alpha blending should be turned on or whether depth testing should be used. 

The commands are as follows:


###Cull
````
Cull Back | Front | Off
````
Set polygon culling mode.


###ZTest
````
ZTest (Less | Greater | LEqual | GEqual | Equal | NotEqual | Always)
````
Set depth buffer testing mode.


###ZWrite
````
ZWrite On | Off
````
Set depth buffer writing mode. 

###Offset
````
Offset OffsetFactor, OffsetUnits
````
Set Z buffer depth offset. See documentation on [Cull and Depth page](SL-CullAndDepth) for more details.

See documentation on [Cull and Depth](SL-CullAndDepth) for more details on Cull, ZTest, ZWrite and Offset.

###Blend
````
Blend sourceBlendMode destBlendMode
Blend sourceBlendMode destBlendMode, alphaSourceBlendMode alphaDestBlendMode
BlendOp colorOp
BlendOp colorOp, alphaOp
AlphaToMask On | Off
````
Sets alpha blending, alpha operation, and alpha-to-coverage modes. See documentation on [Blending](SL-Blend) for more details.


###ColorMask
````
ColorMask RGB | A | 0 | any combination of R, G, B, A
````
Set color channel writing mask. Writing _ColorMask 0_ turns off rendering to all color channels. Default mode is writing
to all channels (RGBA), but for some special effects you might want to leave certain channels unmodified, or disable color
writes completely.

When using multiple render target (MRT) rendering, it is possible to set up different color masks for each render target, by adding index (0-7) at the end. For example, `ColorMask RGB 3` would make render target #3 write only to RGB channels.

### Legacy fixed-function Shader commands

A number of commands are used for writing legacy "fixed-function style" Shaders. This is considered deprecated functionality, as writing [Surface Shaders](SL-SurfaceShaders) or [Shader programs](SL-ShaderPrograms)
allows much more flexibility. However, for very simple Shaders, writing them in fixed-function style can sometimes be easier, so the commands are provided here. Note that all of the following commands are are ignored if you are not using fixed-function Shaders.

#### Fixed-function Lighting and Material
````
Lighting On | Off
Material { Material Block }
SeparateSpecular On | Off
Color Color-value
ColorMaterial AmbientAndDiffuse | Emission
````
All of these control fixed-function per-vertex Lighting: they turn it on, set up Material colors, turn on specular highlights, provide default color (if vertex Lighting is off), and controls how the mesh vertex colors affect Lighting. See documentation on [Materials](SL-Material) for more details.


#### Fixed-function Fog
````
Fog { Fog Block }
````
Set fixed-function Fog parameters. See documentation on[Fogging](SL-Fog) for more details.


#### Fixed-function AlphaTest
````
AlphaTest (Less | Greater | LEqual | GEqual | Equal | NotEqual | Always) CutoffValue
````
Turns on fixed-function alpha testing. See documentation on [alpha testing](SL-AlphaTest) for more details.


#### Fixed-function Texture combiners

After the render state setup, use [SetTexture](SL-SetTexture) commands to specify a number of Textures and their combining modes:

````
SetTexture textureProperty { combine options }
````

## Details

Shader passes interact with Unity's rendering pipeline in several ways; for example, a Pass can indicate that it should only be used for [deferred shading](RenderTech-DeferredShading) using the [Tags](SL-PassTags) command. Certain passes can also be executed multiple times on the same GameObject; for example, in [forward rendering](RenderTech-ForwardRendering) the "ForwardAdd"
pass type is executed multiple times based on how many Lights are affecting the GameObject. See documentation on the [Render Pipeline](SL-RenderPipeline) for more details.


## See also

There are several special passes available for reusing common functionality or implementing various high-end effects:

* [UsePass](SL-UsePass) includes named passes from another shader.
* [GrabPass](SL-GrabPass) grabs the contents of the screen into a Texture, for use in a later pass.


