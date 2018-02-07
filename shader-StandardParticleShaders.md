#Standard Particle Shaders

The Unity Standard Particle Shaders are built-in shaders that enable you to render a variety of particle effects. 

![Standard Particle Unlit Shader](../uploads/Main/StandardParticleUnlitShader.png)

They support many fundamental particle features that you can enable and disable by configuring the Shader in the Material Editor to achieve the effect you want. For example, leaving the __Normal Map__ slot empty disables that feature from the Shader.

##Features

All the Standard Particle Shaders come with a wide range of available Blend Modes. These allow you to combine your particles with the geometry drawn before them in a number of interesting ways.

__Color Modes__ allow you to control how the Albedo Texture is combined with the particle color. 

__Flip-book Mode__ allows you to blend frames together to give smoother animations. 

__Enable Distortion__ allows particles to perform fake refraction with the objects drawn before them. This effect can be quite resource-intensive because it has to capture the current frame to a Texture to work correctly.

There are options for fading out particles when they become close to a surface, and close to the Camera. This is useful for avoiding hard edges when particles intersect with opaque geometry. You can also reduce fill-rate consumption when particles get too close to the Camera.

The following Standard Particle Shaders are provided:

* Standard Particle Unlit Shader to produce special effects
* Standard Particle Surface Shader for geometry that needs to react to light

##Standard Particle Unlit Shader

This is a simple and fast Shader with no lighting calculations. It supports all of the generic particle controls, such as flipbook blending and distortion, but does not perform any lighting calculations.

The following image shows a torch that uses a Standard Particle Unlit Shader with the following properties enabled:

* HDR Color
* Distortion
* Camera Fading
* Blended Flip-Book
* Two Sided

![Flaming torch using a Standard Particle Unlit Shader](../uploads/Main/StandardParticleShader.png)


##Standard Particle Surface Shader

This Shader comes with much of the same functionality as the Standard Shader, but is customised to work well with particles. Like the Standard Shader, it supports __Physically Based Shading__. However, it does not provide Standard Shader features that are unsuitable for dynamic particles, like lightmapping.

![Standard Particle Unlit Shader](../uploads/Main/StandardParticleSurfaceShader.png)

---

* <span class="page-edit">2017-10-16  <!-- include IncludeTextNewPageNoEdit --></span>

* <span class="page-history">Standard Particle Shaders added in [2017.3](https://docs.unity3d.com/2017.3/Documentation/Manual/30_search.html?q=newin20173) <span class="search-words">NewIn20173</span></span>