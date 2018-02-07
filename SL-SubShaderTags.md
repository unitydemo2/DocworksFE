#ShaderLab: SubShader Tags

Subshaders use tags to tell how and when they expect to be rendered to the rendering engine.

## Syntax

````
Tags { "TagName1" = "Value1" "TagName2" = "Value2" }
````

Specifies **TagName1** to have **Value1**, **TagName2** to have **Value2**. You can have as many tags as you like.


## Details


Tags are basically key-value pairs. Inside a [SubShader](SL-SubShader) tags are used to determine rendering order and other parameters of a subshader. Note that the following tags recognized by Unity **must** be inside SubShader section and not inside Pass!

In addition to built-in tags recognized by Unity, you can use your own tags and query them using [Material.GetTag](ScriptRef:Material.GetTag.html) function.


### Rendering Order - Queue tag

You can determine in which order your objects are drawn using the _Queue_ tag. A Shader decides which render queue its objects belong to, this way any Transparent shaders make sure they are drawn after all opaque objects and so on.

There are four pre-defined render queues, but there can be more queues in between the predefined ones. The predefined queues are:

* `Background` - this render queue is rendered before any others. You'd typically use this for things that really need to be in the background.
* `Geometry` _(default)_ - this is used for most objects. Opaque geometry uses this queue.
* `AlphaTest` - alpha tested geometry uses this queue. It's a separate queue from `Geometry` one since it's more efficient to render alpha-tested objects after all solid ones are drawn.
* `Transparent` - this render queue is rendered after _Geometry_ and `AlphaTest`, in back-to-front order. Anything alpha-blended (i.e. shaders that don't write to depth buffer) should go here (glass, particle effects).
* `Overlay` - this render queue is meant for overlay effects. Anything rendered last should go here (e.g. lens flares).



````
Shader "Transparent Queue Example"
{
     SubShader
     {
        Tags { "Queue" = "Transparent" }
        Pass
        {
            // rest of the shader body...
        }
    }
}
````
_An example illustrating how to render something in the transparent queue_

For special uses in-between queues can be used. Internally each queue is represented by integer index; `Background` is 1000, `Geometry` is 2000, `AlphaTest` is 2450, `Transparent` is 3000 and `Overlay` is 4000. If a shader uses a queue like this:

````
Tags { "Queue" = "Geometry+1" }
````

This will make the object be rendered after all opaque objects, but before transparent objects, as render queue index will be 2001 (geometry plus one). This is useful in situations where you want some objects be always drawn between other sets of objects. For example, in most cases transparent water should be drawn after opaque objects but before transparent objects.

Queues up to 2500 ("Geometry+500") are consided "opaque" and optimize the drawing order of the objects for best performance. 
Higher rendering queues are considered for "transparent objects" and sort objects by distance, starting rendering from the furthest ones and ending with the closest ones. Skyboxes are drawn in between all opaque and all transparent objects.



###RenderType tag

`RenderType` tag categorizes shaders into several predefined groups, e.g. is is an opaque shader, or an alpha-tested shader etc. This is used by [Shader Replacement](SL-ShaderReplacement) and in some cases used to produce [camera's depth texture](SL-CameraDepthTexture).


###DisableBatching tag

Some shaders (mostly ones that do object-space vertex deformations) do not work when [Draw Call Batching](DrawCallBatching) is used -- that's because batching transforms all geometry into world space, so "object space" is lost.

`DisableBatching` tag can be used to indicate that. There are three possible values: "True" (always disables batching for this shader), "False" (does not disable batching; this is default) and "LODFading" (disable batching when LOD fading is active; mostly used on trees).


###ForceNoShadowCasting tag

If `ForceNoShadowCasting` tag is given and has a value of "True", then an object that is rendered using this subshader will never cast shadows. This is mostly useful when you are using shader replacement on transparent objects and you do not wont to inherit a shadow pass from another subshader.

###IgnoreProjector tag

If `IgnoreProjector` tag is given and has a value of "True", then an object that uses this shader will not be affected by [Projectors](class-Projector). This is mostly useful on semitransparent objects, because there is no good way for Projectors to affect them.

###CanUseSpriteAtlas tag

Set `CanUseSpriteAtlas` tag to "False" if the shader is meant for sprites, and will not work when they are packed into atlases (see [Sprite Packer](SpritePacker)).


###PreviewType tag

`PreviewType` indicates how the material inspector preview should display the material. By default materials are displayed as spheres, but PreviewType can also be set to "Plane" (will display as 2D) or "Skybox" (will display as skybox).


##See Also

Passes can be given Tags as well, see [Pass Tags](SL-PassTags).
