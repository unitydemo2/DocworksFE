Projector
=========


A __Projector__ allows you to project a __Material__ onto all objects that intersect its frustum. The material must use a special type of shader for the projection effect to work correctly - see the projector prefabs in Unity's standard assets for examples of how to use the supplied Projector/Light and Projector/Multiply shaders.


![](../uploads/Main/Inspector-Projector.png) 

Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Near Clip Plane__ |Objects in front of the near clip plane will not be projected upon. |
|__Far Clip Plane__ |Objects beyond this distance will not be affected. |
|__Field Of View__ |The field of view in degrees. This is only used if the Projector is not Ortho Graphic. |
|__Aspect Ratio__ |The Aspect Ratio of the Projector. This allows you to tune the height vs width of the Projector. |
|__Is Ortho Graphic__ |If enabled, the Projector will be Ortho Graphic instead of perspective. |
|__Ortho Graphic Size__ |The Ortho Graphic size of the Projection. this is only used if Is Ortho Graphic is turned on. |
|__Material__ |The Material that will be Projected onto Objects. |
|__Ignore Layers__ |Objects that are in one of the Ignore Layers will not be affected. By default, Ignore Layers is none so all geometry that intersects the Projector frustum will be affected. |


Details
-------


With a projector you can:

1. Create shadows.
1. Make a real world projector on a tripod with another [Camera](class-Camera) that films some other part of the world using a __Render Texture__.
1. Create bullet marks.
1. Funky lighting effects.


![A Projector is used to create a Blob Shadow for this Robot](../uploads/Main/Projector-BlobShadow.png) 

If you want to create a simple shadow effect, simply drag the __StandardAssets-&gt;Blob-Shadow-&gt;Blob shadow projector__ __Prefab__ into your scene. You can modify the Material to use a different Blob shadow texture.

**Note:** When creating a projector, always be sure to set the wrap mode of the texture's material of the projector to _clamp_. else the projector's texture will be seen repeated and you will not achieve the desired effect of shadow over your character.
Hints
-----


* Projector Blob shadows can create very impressive Splinter Cell-like lighting effects if used to shadow the environment properly.
* When no __Falloff__ Texture is used in the projector's Material, it can project both forward and backward, creating "double projection". To fix this, use an alpha-only Falloff texture that has a black leftmost pixel column.
