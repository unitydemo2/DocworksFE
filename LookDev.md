# Look Dev

##Introduction

Look Dev is an experimental image-based lighting tool that allows you to check and compare different Assets through a viewer to ensure they are correctly authored for various lighting conditions. It also allows you to debug Assets where required. Load Assets in as Prefabs for the best experience.

## Asset validation

Asset validation is the process of confirming that Assets are authored correctly so they behave as expected in different lighting environments.

You must validate using HDRI. HDRI is a type of real-world lighting with incredibly high detail. As such, it offers a perfect lighting rig that would be difficult to create by hand. By using such an accurate lighting environment to test an Asset, you can determine whether the Asset itself or the game’s lighting is causing any poor visual quality.

To learn more about creating HDRI environments, see documentation on the [HDRI view](LookDevHDRIView).

Look Dev allows you to load two different Assets in two different views. This is useful for comparison. For example, an Art Director can check that a new Asset matches the art direction guidelines of a reference Asset. 

## Who should use Look Dev? 

Look Dev is mainly designed for texture artists, modelling artists, lighting artists, artistic directors, outsourcing managers and anybody else involved in the visual art style of a project. 

Rather than using multiple tools to visualise and validate new content, Look Dev allows everybody to visualize the Asset the same way. This means that you can validate the Asset immediately because how it appears in the tool is the same as how it appears in the finished project. 

Note that while Look Dev is intended for artists, it is not an artistic tool. It is only intended to be used for Asset visualization and validation.

## Initial setup

Before using Look Dev, you need to make sure Unity is set up for the best results:

* Go to __Player Settings__ (menu: __Edit__ > __Project Settings__ > __Player__) and navigate to __Other Settings__. 
* Set the __Rendering Path__ to __Deferred__ and the __Color Space__ to __Linear__. 

Look Dev always uses these settings, independently of the project settings, so changing these settings in your project ensures that what you see in the Look Dev viewer matches what you see in the Scene view. 

##Known issues

When a skybox uses a cube map with a specular convolution type, it produces a blurry result in smaller rendering windows. Use a large window when using Look Dev in this context.

![Known issue: skybox can produce a blurry result in certain circumstances](../uploads/Main/LookDev-KnownIssueSkybox.png)
