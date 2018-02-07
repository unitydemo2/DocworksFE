#Size by Speed module

This module allows you to create particles that change size according to their speed in distance units per second.


![](../uploads/Main/PartSysSizeBySpeed.png)

##Properties

|**_Property_** |**_Function_** |
|:---|:---|
|__Separate Axes__ |Control the particle size independently on each axis. |
|__Size__ |A curve defining the particle's size over a speed range. |
|__Speed Range__ |The low and high ends of the speed range to which the size curve is mapped (speeds outside the range will map to the end points of the curve). |

##Details

Some situations will require particles which vary in size depending on their speed. For example, you would expect small pieces of debris to be accelerated more by an explosion than larger pieces. You can achieve effects like this using __Size By Speed__ with a simple ramp curve that proportionally increases the speed as the size of the particle decreases. Note that this should not be used with the __Limit Velocity Over Lifetime__ module, unless you want particles to change their size as they slow down.

__Speed Range__ specifies the range of values that the X (width), Y (height) and Z (depth) shapes apply to. The Speed Range is only applied when the size is in one of the curve modes. Fast particles will scale using the values at the right end of the curve, while slower particles will use values from the left side of the curve. For example, if you specify a Speed Range between 10 and 100:

* Speeds below 10 will set the Particle size corresponding with the left-most edge of the curve.
* Speeds above 100 will set the Particle size corresponding with the right-most edge of the curve.
* Speeds between 10 and 100 will set the Particle size determined by the point along the curve corresponding to the Speed. In this example, a Speed of 55 would set the size according to the midpoint of the curve.

##Non-uniform particle scaling


![](../uploads/Main/PartSysSizeBySpeed-SepAxes.png)

You can specify how a particle’s width, height and depth size changes by speed independently. In the __Size by Speed__ module, check the __Separate Axes__ checkbox, then choose how the X (width), Y (height) and Z (depth) of the particle is affected by the speed of the particle. Remember that Z will only be used for Mesh particles.