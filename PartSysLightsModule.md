# Lights module

Add real-time lights to a percentage of your particles using this module.

![](../uploads/Main/PartSysLightsModule.png)

## Properties

| Property| Function |
|:---|:---| 
| __Light__| Assign a [Light](LightingInUnity) Prefab describing how your particle lights should look. |
| __Ratio__| A value between 0 and 1 describing the proportion of particles that will receive a light. |
| __Random Distribution__| Choose whether lights are assigned randomly or periodically. When set to true, every particle has a random chance of receiving a light based on the Ratio. Higher values increase the probability of a particle having a light. When set to false, the Ratio controls how often a newly created particle receives a light (for example, every Nth particle will receive a light). |
| __Use Particle Color__| When set to True, the final color of the Light will be modulated by the color of the particle it is attached to. If set to False, the Light color is used without any modification. |
| __Size Affects Range__| When enabled, the __Range__ specified in the Light will be multiplied by the size of the particle. |
| __Alpha Affects Intensity__| When enabled, the __Intensity__ of the light is multiplied by the particle alpha value. |
| __Range Multiplier__| Apply a custom multiplier to the Range of the light over the lifetime of the particle using this curve. |
| __Intensity Multiplier__| Apply a custom multiplier to the Intensity of the light over the lifetime of the particle using this curve. |
| __Maximum Lights__| Use this setting to avoid accidentally creating an enormous number of lights, which could make the Editor unresponsive or make your application run very slowly. |

## Details

The Lights module is a fast way to add real-time lighting to your particle effects. It can be used to make systems cast light onto their surroundings, for example for a fire, fireworks or lightning. It also allows you to have the lights inherit a variety of properties from the particles they are attached to. This can make it more believable that the particle effect itself is emitting light. For example, this can be achieved by making the lights fade out with their particles and having them share the same colors.

This module makes it easy to create a lot of real-time lights very quickly, and real-time lights have a high performance cost, especially in Forward Rendering mode. If the lights also cast shadows, the performance cost is even higher. To help guard against an accidental tweak to the emission rate and thus causing thousands of real-time lights to be created, the Maximum Lights property should be used. Creating more lights than your target hardware is able to manage can cause slowdowns and unresponsiveness.