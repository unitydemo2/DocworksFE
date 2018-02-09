Upgrading to Unity 5.2
=================

Global Illumination
-------------------

UV packing for baked UVs not filling the 0-1 space (smaller or bigger) has been fixed. It makes the resolution assigned to each object work much more reliably if that object's unwrap is not filling the 0-1 space and also when its bounds are non-square. Please review the resolution on your instances for baked lightmaps.

Shader variant stripping was fixed for realtime lightmaps. Now each lightmaps mode (non-directional, directional and directional specular) variant can be picked for baked and realtime GI separately. Please review your settings if you previously selected a specific lightmaps mode variant in the Graphics Settings to make that mode work for realtime lightmaps.

Bounce scale has been changed from the arbitrary value of 0.7 to 1.0. The bounce is the product of the albedo and bounce scale. Artists should set real-life albedo values (the brightest non-metallic is snow with 0.9). This is our PBS reference [http://forum.unity3d.com/threads/official-5-0-pbr-calibration-charts.289416/](http://forum.unity3d.com/threads/official-5-0-pbr-calibration-charts.289416/)

Since you should author physically correct albedo, it makes sense for us to set the scale close to 1. We already clamp albedo values in the meta pass, so the bounce scale should just be 1.0f.

Please note that if you choose to set albedo to 1.0 in a custom meta pass without clamping, then the scene can look like it's exploding with light.

Shaders
-------

"Fixed Function" style shaders (the ones that use SetTexture, Lighting On etc.) internally get turned into actual shaders at shader import time now. Upside is that they now work on all platforms (previously did not work on consoles), and with more consistency. Also a lot of code and fixed function related inefficiencies got removed from runtime, making rendering a bit faster. Downside is, creating fixed function shaders at runtime - using ``new Material(fixedFunctionShaderString)`` - does not work anymore. That constructor was deprecated in Unity 5.1, and now in 5.2 it actually stopped working for fixed function shaders.

Reflection Probes
-----------------

We've changed how Reflection Probes are rendered when using Deferred Shading, in order to allow "screen space reflections" effects in the future. Short version is: in deferred shading, reflection probes are per-pixel instead of per-object now.

*Comparison of current behavior (reflection probes per object; in some cases hard to avoid harsh reflection transitions between large objects) and reflection probes per pixel (transitions much less visible; and they happen at probe boundaries not at object boundaries):*

![](../uploads/ReflectionProbeComparison.png)

Before (5.0 and 5.1)

* Reflection probes are sampled during the G-buffer pass, in exactly the same way as in forward rendering. They are written into "emission" buffer together with light probes, lightmaps and emissive material parts.

* This meant you get one (or two, when probe blending is on) reflection probes *per object*.

* Reflections being together with emission/lightmaps in the same buffer means that doing SSRR "properly" is hard. SSRR provides reflections by itself (and falls back to reflection probes where it can't), but it does not know which part of "emission buffer" color is coming from reflection probes.

Now (5.2)

* When using deferred shading, do not sample reflection probes during G-buffer pass.

* Instead, after the G-buffer is done, make a separate "deferred reflections" pass that draws reflection probes as boxes in screenspace; that output reflection information into a separate render target.

* *[Future: SSRR effect will use this separate reflections buffer]*

* Combine reflections buffer & emission buffer at the end.

What does this mean? *(everything below only affects deferred shading)*

* **Reflection probes are no longer per-object**; they are effectively per-pixel. It is easier to have large objects affected by many reflection probes.
    * Also probes got a "blend distance" which defines how much space around the probe is used for blending into other probes.
    * Smaller probes "override" larger ones.

* **Reflection probe Renderer flags (probe blending, etc.) are ignored**; everything is affected by reflection probes in the same way (since it happens in screenspace now). This is very similar to how "receive shadows" flag is ignored in deferred shading.

* Your custom-written shaders that do deferred shading should mostly continue to work (in the worst case, they will be sampling a black reflection cubemap). If you do some totally crazy stuff in shaders, they might need to be updated to work with deferred shading in 5.2.
    * If you are using custom deferred shading light pass shader (with custom BRDF etc.), you’ll probably want to use custom deferred reflections shader too, with the same BRDF applied to reflection probes.

Shuriken
----------------------

Particles are now generated in world space, which may require an update to any custom vertex shaders. This change was made in order to allow re-use of the particle buffers between each eye for VR.

Mesh particles now support the Texture Sheet Animation module. It's worth checking that your existing effects do not have this enabled by accident, otherwise you may see a change in behaviour.

The Dampen parameter in the Limit Velocity over Lifetime module used to have a stronger effect at higher framerates. This has been fixed, and if your game is targetting 30fps, your old effects will be unaffected by this change. However, if your game targets a differnet FPS, you can update the Dampen value using this formula, to ensure your effect is unchaged in 5.2:

    newDampen = 1.0f - pow(1.0f - oldDampen, targetFPS / 30.0f);

Graphics (Other items)
----------------------

``Material.CopyPropertiesFromMaterial`` now also copies shader keywords and render queue. If you were relying on them being not copied, you’ll have to change your code.

SpeedTree materials now need to be re-generated as there are changes to SpeedTree built-in shaders. You could do so by selecting SpeedTree prefabs in your project and hit "Apply & Generate Materials" button. *Please be noted that by doing so your customisations to the generated material assets (if any) will be overwritten.*

UI
--

In 5.2 we have combined the shaders that text and normal UI element rendering users. A side effect of this is that if you specify a manual font texture in a 32bit format then the color channels will be honored. This means that black texture channels will result in black text where previously the text would be white (we only looked at the alpha). If you wish to use custom textures for your fonts do one of the following:

1. Change the import format of the texture to A8. This will only keep the alpha component and Unity will generate the text as white by default.
1. Specify a color / colors in the texture for Unity to use when rendering the text

Multiplayer
-----------

The way the project identification is handled has changed in Unity 5.2, now the project is automatically registered and you do not need to manually enter an ID anywhere. There is a Multiplayer panel in the Services Window (open it with cloud icon in upper right corner) and in there you can find a deep link directly to the project on the website (Go to dashboard). When configured the Multiplayer configuration will appear here.

![](../uploads/Main/MultiplayerServicesWindowUG.png)

