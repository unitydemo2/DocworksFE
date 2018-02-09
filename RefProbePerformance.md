#Reflection Probe Performance and Optimisation

Rendering a reflection probe's cubemap takes a significant amount of processor time for a number of reasons:

* Each of the six cubemap faces must be rendered separately using a "camera" at the probe's origin.
* The probes will need to be rendered a separate time for each reflection bounce level (see the [Interreflections](AdvancedRefProbe) topic for further details).
* The various mipmap levels of the cubemap must undergo a blurring process to allow for glossy reflections. 

The time taken to render the probes affects the baking workflow in the editor and, more importantly, runtime performance of the player. Below are some tips for keeping the performance impact of reflection probes to a minimum.


##General Tips

The following issues affect both offline baking _and_ runtime performance.

###Resolution

The higher the resolution of a cubemap, the greater will be its rendering time. You can optimise probes by setting lower resolutions in places where the reflection detail is less important (for example, if a reflective object is small and/or distant then it will naturally show less detail). Higher resolutions should still be used wherever the detail will be noticeable.

###Culling Mask

A standard technique to improve a normal camera's performance is to use the _Culling Mask_ property to avoid rendering insignificant objects; the technique works equally well for reflection probes. For example, if your scene contains many small objects (eg, rocks and plants) you might consider putting them all on the same layer and then using the culling mask to avoid rendering them in the reflection. 

###Texture compression

To optimize the rendering time and lower the GPU memory consumption, texture compression should always be used. To control texture compression for baked Reflection Probes, open the Lighting window (menu: __Window__ > __Lighting__ > __Settings__), navigate to __Environmental Lighting__ > __Reflections__ and use the __Compression__ drop-down menu. Note that real-time Reflection Probes are not compressed in memory, and their size in memory depends on __Resolution__ and __HDR__ settings. Because of this, sampling real-time Reflection Probes is usually more resource-intensive than sampling baked Reflection Probes.

##Real-time Probe Optimisation

The rendering overhead is generally more significant at for real-time probes than for those baked in the editor. Updates are potentially quite frequent and this can have an impact on framerate if not managed correctly. With this in mind, real-time probes provide the following properties to let you handle probe rendering as efficiently as possible.

###Refresh Mode

The __Refresh Mode__ lets you choose when the probe will update. The most resource-intensive option in terms of processor time is __Every Frame__. This gives the most frequent updates with minimal programming effort but you may encounter performance problems if you use this mode for all probes.

If the mode is set to _On Awake_, the probe will be updated at runtime but only once at the start of the scene. This is useful if the scene (or part of it) is set up at run-time but does not change during its lifetime.

The final mode, __Via Scripting__, lets you control probe updates from a script. Although some effort is involved in coding the script, this approach does allow for useful optimisations. For example, you might update a probe according to the apparent size of passing objects (ie, small objects or large objects at a distance are not worth an update).


###Time Slicing
When the _Refresh Mode_ described above is set to _Every Frame_ the processing load can be considerable. _Time Slicing_ allows you to spread the cost of updates over several frames and thereby reduce the load at any given time. This property has three different options:

* **All Faces at Once** will cause the six cubemap faces to be rendered immediately (on the same frame) but then the blurring operation for each of the six first level mipmaps will take place on separate frames. The remaining mipmaps will then be blurred on a single frame and the results copied to the cubemap on another frame. The full update therefore takes nine frames to complete.

* **Individual Faces** works the same way as _All Faces at Once_ except that the initial rendering of each cubemap face takes place on its own frame (instead of all six on the first frame). The full update takes fourteen frames to complete; this option has the lowest impact on framerate but the relative long update time might be noticeable when, say, lighting conditions change abruptly (eg, a lamp is suddenly switched on).

* **No Time Slicing** disables the time slicing operation completely and so each probe update takes place within a single frame. This ensures that the reflections are synchronised exactly with the appearance of surrounding objects but the processing cost can be prohibitive.

As with the other optimisations, you should consider using the lower-quality options in places where reflections are less important and save the _No Time Slicing_ option for places where the detail will be noticed.



