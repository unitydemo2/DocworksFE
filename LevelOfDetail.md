#Level of Detail (LOD)

When a GameObject in the scene is a long way from the camera, the amount of detail that can be seen on it is greatly reduced. However, the same number of triangles will be used to render the object, even though the detail will not be noticed. An optimisation technique called _Level Of Detail_ (LOD) rendering allows you to reduce the number of triangles rendered for an object as its distance from the camera increases. As long as your objects aren't all close to the camera at the same time, LOD will reduce the load on the hardware and improve rendering performance.

In Unity, you use the __LOD Group__ component to set up LOD rendering for an object. Full details are given on the [component reference page](class-LODGroup) but the images below show how the LOD level used to render an object changes with its distance from camera. The first shows LOD level 0 (the most detailed). Note the large number of small triangles in the mesh:

![camera at LOD 0](../uploads/Main/LOD0Image.png)

The second shows a lower level being used when the object is farther away. Note that the mesh has been reduced in detail (smaller number of larger triangles):

![camera at LOD 1](../uploads/Main/LOD1Image.png) 

Since the arrangement of LOD levels depends somewhat on the target platform and available rendering performance, Unity lets you set maximum LOD levels and a LOD bias preference (ie, whether to favour higher or lower LOD levels at threshold distances) in the [Quality Settings](class-QualitySettings).


##LOD Naming Convention for Importing Objects

If you create a set of meshes with names ending in \_LOD0, \_LOD1, \_LOD2, etc, for as many LOD levels as you like, a LOD group for the object with appropriate settings will be created for you automatically on import. For example, if the base name for your mesh is _Player_, you could create files called _Player\_LOD0_, _Player\_LOD1_ and _Player\_LOD2_ to generate an object with three LOD levels. The numbering convention assumes that LOD 0 is the most detailed model and increasing numbers correspond to decreasing detail.
