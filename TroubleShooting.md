# Troubleshooting

This section addresses common problems that can arise when using Unity. Each platform is dealt with separately below.

## Platform-specific troubleshooting

### Geforce 7300GT on OSX 10.6.4

Deferred rendering is disabled because materials are not displayed correctly for Geforce 7300GT on OX 10.6.4; This happens because of buggy video drivers.

### On Windows x64, Unity crashes when script throws a NullReferenceException

You need to apply [Windows hotfix #976038](http://support.microsoft.com/kb/976038).

## Script editing

###MonoDevelop: Disabling the welcome page 

In the MonoDevelop preferences, go to the Visual Style section, and uncheck "Load welcome page on startup".

### Script opens in MonoDevelop, even when Visual Studio is set as the script editor

This happens when Visual Studio reports that it failed to open your script. The most common cause for this is an external plugin (such as Resharper) displaying a dialog at startup, requesting input from the user. This causes Visual Studio to report that it failed to open.

## Graphics

###Slow framerate and/or visual artifacts

This may occur if your video card drivers are not up to date. Make sure you have the latest official drivers from your card vendor.

## Shadows

* Shadows require certain graphics hardware support. See [Light Performance](LightPerformance) page for details.
* Make sure shadows are enabled in [Quality Settings](class-QualitySettings).
* Shadows on Android and iOS have limitations: soft shadows are not available, and in forward rendering path only a single directional light can cast shadows. There is no limit to the number of lights casting shadows in the deferred rendering path.

### Some GameObjects do not cast or receive shadows

An object's [Renderer](class-MeshRenderer) must have __Receive Shadows__ enabled for shadows to be rendered onto it. Also, an object must have __Cast Shadows__ enabled in order to cast shadows on other objects (both are on by default).

Only opaque objects cast and receive shadows. This means that objects using the built-in [Transparent](shader-TransparentFamily) or Particle shaders will not cast shadows. In most cases it is possible to use [Transparent Cutout](shader-TransparentCutoutFamily) shaders for objects like fences, vegetation, etc. If you use custom written [Shaders](Shaders), they have to be pixel-lit and use the [Geometry render queue](SL-SubShaderTags). Objects using __VertexLit__ shaders do not receive shadows but are able to cast them.

Only __Pixel lights__ cast shadows. If you want to make sure that a light always casts shadows no matter how many other lights are in the scene, then you can set it to __Force Pixel__ render mode (see the [Light](class-Light) reference page).
