#Spatial mapping concepts

__Spatial mapping__ is the process of mapping real-world objects into the virtual world. This is a great way to provide better real-world interaction to your Windows Holographic application.

##Mapping

The __HoloLens__ device constantly scans its surroundings and refines its understanding of the world based on new sensor data. Updates occur frequently, so that the device can pick up environmental changes such as people moving through the room or doors opening and closing. The world mapping data set is saved on the device and persists across multiple applications and device restarts. 

Transparent, black, and reflective surfaces are largely invisible to the device. If the device can't detect something, it usually leaves an empty patch within the spatial mapping data. The same is true for parts of the world that it hasn't been in or can't see. For example, no data exists for rooms that it hasn't observed.

##Data organization

The device's world mapping is chopped up into regularly-sized chunks called __Surfaces__. __Surfaces__ are oriented in the world in a way convenient to the system. There's no guarantee that __Surfaces__ are arranged in any particular orientation, and they may not intersect a given world space, such as a room, in a good way. Data generated for a __Surface__ overlaps neighboring __Surfaces__ slightly.

Note that there is no semantic meaning or interpretation associated with any of the __Surface__ data. The system does not know and cannot report on what's in a __Surface__. 

For example: the system cannot tell you that the blob on the desk is a mug, or what the vaguely chair-like object in the middle of the room is. It only reports on the configuration of the geometry in that area based on its understanding of the world, which is gleaned from its sensory input.

##Observers

You access spatial mapping data through a [SurfaceObserver](ScriptRef:XR.WSA.SurfaceObserver.html). This is a volume describing a view into the system's spatial mapping world. A __SurfaceObserver__ can report on the set of __Surfaces__ it intersects with that have been added, changed, or removed. This is the main API point for working with spatial mapping data.

##Points to note

You need to be aware of the following issues. They are due to how the system works. 

1.  The amount of spatial mapping data can be very large, which poses scalability challenges.
2.  Objects or people moving quickly within the room can make the data very irregular.
3.  Holes in the data can sometimes cause issues, particularly if you need continuous data for design reasons.

See Microsoft's documentation on [Spatial mapping](https://dev.windows.com/en-us/holographic/spatial_mapping) to learn more about spatial mapping concepts.