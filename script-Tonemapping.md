#Tonemapping


__Tonemapping__ is usually understood as the process of mapping color values from [HDR](HDR) (high dynamic range) to LDR (low dynamic range). In Unity, this means for most platforms that arbitrary 16-bit floating point color values will be mapped to traditional 8-bit values in the [0,1] range.

Note that Tonemapping will only properly work if the used camera is [HDR](HDR) enabled. It is also recommended to give light sources higher than normal intensity values to make use of the bigger range. Just as in real life there is huger differences in Luminance and our eyes or any capturing medium is only able to sample a certain range of that. 

Tonemapping works well in conjunction with the HDR-enabled [Bloom image effect](script-Bloom). Make sure that Bloom should be applied before Tonemapping as otherwise all high ranges will be lost. Generally, any effect that can benefit from higher luminances should be scheduled before the Tonemapper (one more example being the [Depth of Field image effect](script-DepthOfField)).

There are different ways on how to map intensities to LDR (as selected by __Mode__). This effect provides several techniques, two of them being adaptive (__AdaptiveReinhard__ and __AdaptiveReinhardAutoWhite__), which means that color changes are carried out delayed as the change in intensities is fully registered. Cameras and the human eye have this effect. This enables interesting dynamic effects such as a simulation of the natural adaption happening when entering or leaving a dark tunnel into bright sunlight.

The following two screenshots show Photographic Tonemapping with different exposure values. Note how banding is avoided by using HDR cameras.


![](../uploads/ImageEffects/Photographics.png) 



![](../uploads/ImageEffects/Photographics2.png) 

As with the other [image effects](comp-ImageEffects), you must have the [Standard Assets Effects package](HOWTO-InstallStandardAssets) installed before it becomes available.

##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Mode__ |Choose the desired tonemapping algorithm.|


| | |
|:---|:---|
|__Exposure__ |Simulated exposure, defining the actual range of luminances.|
|__Average grey__ |Average grey value of the scene that defines the intensity of the result.|
|__White__ |Smallest value that will be mapped white.|
|__Adaption speed__ |Adjustment speed for all adaptive tonemappers.|
|__Texture size__ |Size of the internal texture for all adaptive tonemappers. Bigger values capture more details when calculating the new intensity and lower performance.|

##Hardware Support

This effect should run on all hardware that Unity supports.
