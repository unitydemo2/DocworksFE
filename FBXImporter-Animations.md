FBX Importer - Animations Tab
=============================



![](../uploads/Main/MecanimImporterAnimationsTab.png) 


|     |     |
| --- | --- |
| **Animations** |  |
| __Bake Animations__ |Enable this when using IK or simulation in your animation package. Unity will convert to forward kinematics on import. This option is available only for Maya, 3dsMax and Cinema4D files. |
| __Anim. Compression__ | The type of compression that will be applied to this mesh's animation(s) |
| &#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Off__ | Disables animation compression. This means that Unity doesn't reduce keyframe count on import, which leads to the highest precision animations, but slower performance and bigger file and runtime memory size. It is generally not advisable to use this option - if you need higher precision animation, you should enable keyframe reduction and lower allowed __Animation Compression Error__ values instead. |
| &#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Keyframe Reduction__ |Reduces keyframes on import. If selected, the __Animation Compression Errors__ options are displayed. |
| &#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Keyframe Reduction and Compression__ | Reduces keyframes on import and compresses keyframes when storing animations in files. This affects only file size - the runtime memory size is the same as __Keyframe Reduction__. If selected, the __Animation Compression Errors__ options are displayed.  |
| &#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Optimal__ | Used for generic and humanoid rig. |
| __Animation Compression Errors__ | These options are available only when keyframe reduction or Optimal compression is enabled. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Rotation Error__|Defines how much rotation curves should be reduced. The smaller value you use - the higher precision you get. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Position Error__|Defines how much position curves should be reduced. The smaller value you use - the higher precision you get. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Scale Error__|Defines how much scale curves should be reduced. The smaller value you use - the higher precision you get. |

For properties of AnimationClip, go to the [AnimationClip reference page](class-AnimationClip)
