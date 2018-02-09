#Color By Speed module

The color of a particle can be set here to change according to its speed in distance units per second.

![](../uploads/Main/PartSysColorBySpeedInsp.png)

##Properties

|**_Property_** |**_Function_** |
|:---|:---|
|__Color__ |The color gradient of a particle defined over a speed range. |
|__Speed Range__ |The low and high ends of the speed range to which the color gradient is mapped (speeds outside the range will map to the end points of the gradient). |

##Details
Burning or glowing particles (such as sparks) tend to burn more brightly when they move quickly through the air (for example, when sparks are exposed to more oxygen), but then dim slightly as they slow down. To simulate this, you might use _Color By Speed_ with a gradient that has white at the upper end of the speed range, and red at the lower end (in the spark example, faster particles will appear white while slower particles are red).
