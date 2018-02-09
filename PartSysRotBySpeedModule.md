#Rotation By Speed module

The rotation of a particle can be set here to change according to its speed in distance units per second.

![](../uploads/Main/PartSysRotBySpeedInsp.png)

##Properties

|**_Property_** |**_Function_** |
|:---|:---|
|__Separate Axes__ |Control rotation independently for each axis of rotation. |
|__Angular Velocity__ |Rotation velocity in degrees per second. |
|__Speed Range__ |The low and high ends of the speed range to which the size curve is mapped (speeds outside the range will map to the end points of the curve). |

##Details

This property can be used when the particles represent solid objects moving over the ground such as rocks from a landslide. The rotation of the particles can be set in proportion to the speed so that they roll over the surface convincingly.

The Speed Range is only applied when the velocity is in one of the curve modes. Fast particles will rotate using the values at the right end of the curve, while slower particles will use values from the left side of the curve.