# Noise module

Add turbulence to particle movement using this module.

![](../uploads/Main/PartSysNoiseModule.png)

## Properties

| Property| Function |
|:---|:---| 
| __Separate Axes__| Control the strength and remapping independently on each axis. |
| __Strength__| A curve that defines how strong the noise effect is on a particle over its lifetime. |
| __Frequency__| Low values create soft, smooth noise, and high values create rapidly changing noise. |
| __Scroll Speed__| Move the noise field over time to cause more unpredictable and erratic particle movement. |
| __Damping__| When enabled, strength is proportional to frequency. Tying these values together means the noise field can be scaled while maintaining the same behaviour, but at a different size. |
| __Octaves__| Specify how many layers of overlapping noise are combined to produce the final noise values. Using more layers gives richer, more interesting noise, but significantly adds to the performance cost. |
| __Octave Multiplier__| For each additional noise layer, reduce the strength by this proportion. |
| __Octave Scale__| For each additional noise layer, adjust the frequency by this multiplier. |
| __Quality__| Lower quality settings reduce the performance cost significantly, but also affect how interesting the noise looks. Use the lowest quality that gives you the desired behavior for maximum performance. |
| __Remap__| Remap the final noise values into a different range. |
| __Remap Curve__| The curve that describes how the final noise values are transformed. For example, you could use this to pick out the lower ranges of the noise field and ignore the higher ranges by creating a curve that starts high and ends at zero. |

## Details

Adding noise to your particles is a simple and effective way to create interesting patterns and effects. For example, imagine how embers from a fire move around, or how smoke swirls as it moves. Strong, high frequency noise could be used to simulate the fire embers, while soft, low frequency noise would be better suited to modeling a smoke effect.

For maximum control over the noise, you can enable the Separate Axes option. This allows you to control the strength and remapping on each axis independently.