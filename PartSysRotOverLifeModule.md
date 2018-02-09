# Rotation Over Lifetime module

Here, you can configure particles to rotate as they move.

![](../uploads/Main/PartSysRotOverLifeModule1.png)

## Properties

| Property| Function |
|:---|:---| 
| __Separate Axes__| Allow rotation to be specified per axis. When this is enabled, the option to set a rotation for each of X, Y and Z is presented. |
| __Angular Velocity__| Rotation velocity in degrees per second. See below for more information. |

## Details

This setting is useful when particles represent small solid objects, such as pieces of debris from an explosion. Assigning random values of rotation will make the effect more realistic than having the particles remain upright as they fly. The random rotations will also help to break up the regularity of similarly shaped particles (the same texture repeated many times can be very noticeable).

![Leaves rendered using particles with random 3D rotation](../uploads/Main/PartSysRotOverLifeModule2.gif)

## Options

The angular velocity option can be changed from the default constant speed. The drop-down to the right of the velocity can provide:

| Property| Function |
|:---|:---| 
| __Constant__| The velocity for particle rotation in degrees per second. |
| __Curve__| The angular velocity can be set to change over the lifetime of the particle. A curve editor appears at the bottom of the Inspector which allows you to control how the velocity changes throughout the lifetime of the particle (see Image A below). If the Separate Axes box is ticked, each of the X, Y and Z axes can be given curved velocity values. |
| __Random Between Two Constants__| The angular velocity properties has two angles allowing a rotation between them. |
| __Random Between Two Curves__| The angular velocity can be set to change over the lifetime of the particle specified by a curve. In this mode, two curves are editable, and each particle will pick a random curve between the range of these two curves that you define (see Image B below). |


![](../uploads/Main/PartSysRotOverLifeModule3.png)

Image A: Z-axis angular velocity


![](../uploads/Main/PartSysRotOverLifeModule4.png)

Image B: Angular velocity between two curves