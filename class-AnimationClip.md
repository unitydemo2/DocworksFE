Animation Clip
==============


__Animation Clips__ are the smallest building blocks of animation in Unity. They represent an isolated piece of motion, such as RunLeft, Jump, or Crawl, and can be manipulated and combined in various ways to produce lively end results (see [Animation State Machines](AnimationStateMachines), [Animator Controller](class-AnimatorController), or [Blend Trees](class-BlendTree)). 
Animation clips can be selected from imported FBX data (see [FBXImporter settings for Animations](FBXImporter-Animations)), and when you click on the set of available animation clips you will see the following set of properties: 

![The Animation Clip Inspector](../uploads/Main/classAnimationClip-Inspector.png) 

##Asset-specific properties

(These properties apply to all animation clips defined within this asset).

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Import Animation__ |Should any animation be imported from this asset?. If un-checked, all other options on this page are hidden and no animation is imported.|
|__Bake Animations__ |Animations created using IK or Simulation will be baked to forward kinematic keyframes. This option is only available for Maya, 3dsMax and Cinema4D files. |
|__Resample Curves__ |When enabled, animation curves will be resampled on every frame. You should enable this if you're having issues with the interpolation between keys in your original animation. Disable this to keep animation curves as they were originally authored. This option is only available for Generic animtions, not Humanoid animations.|
|__Import Animation__ |Should any animation be imported from this asset?. If un-checked, all other options on this page are hidden and no animation is imported.|
|__Anim. Compression__ |The type of compression to use when importing the animation|
| - __Off__ |No Compression|
| - __Keyframe Reduction__ |Removes redundant keyframes|
| - __Optimal__ |Let unity decide how to compress. Either by keyframe reduction or by using dense format. Unity will pick the most optimal of the two.|

------------------------------

##Clip-specific properties

(These properties are set separately for each animation clip defined within this asset).

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Name__ |The name of the clip.|
|__Source Take__ |The take in the source file to use as a source for this animation clip. (This option will not show up if there's only one take). This is what defines a set of animation as separated in Motionbuilder, Maya and other 3D packages. Unity can import these takes as individual clips or you can create them from the whole file or a take. |
|__Start__ |Start frame of the clip.|
|__End__ |End frame of the clip.|
|__Loop Time__ |Enable this option to make the animation clip play through and restart when the end is reached.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Loop Pose__ |Enable to make the motion loop seamlessly.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Cycle Offset__ |Offset to the cycle of a looping animation, if we want to start it at a different time.|
|__Root Transform Rotation__ | | 
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Bake into Pose__ |Enable to make root rotation be baked into the movement of the bones. Disable to make root rotation be stored as root motion.| 
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Based Upon__ |What the root rotation is based upon.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; - __Original__|Keeps the rotation as it is authored in the source file.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; - __Body Orientation__ |Keeps the upper body pointing forward.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Offset__ |Offset to the root rotation (in degrees).|
|__Root Transform Position (Y)__ | | 
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Bake into Pose__ |Enable to make vertical root motion be baked into the movement of the bones. Disable to make vertical root motion be stored as root motion.| 
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Based Upon__ |What the vertical root position is based upon.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; - __Original__ |Keeps the vertical position as it is authored in the source file.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; - __Center of Mass__ |Keeps the center of mass aligned with root transform position.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; - __Feet__|Keeps the feet aligned with the root transform position.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Offset__ |Offset to the vertical root position.|
|__Root Transform Position (XZ)__ | | 
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Bake into Pose__ |Enable to make horizontal root motion be baked into the movement of the bones. Disable to make horizontal root motion be stored as root motion.| 
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Based Upon__ |What the horizontal root position is based upon.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; - __Original__ |Keeps the horizontal position as it is authored in the source file.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; - __Center of Mass__ |Keeps the center of mass aligned with the root transform position.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Offset__ |Offset to the horizontal root position.|
|__Mirror__ |Mirror left and right in this clip. (Only available for Humanoid Animations)|
|__Additive Reference Pose__ |When enabled, allows you to define the reference pose used as the base for the additive animation. Also, a blue marker becomes visible in the Start/End timeline editor: ![](../uploads/Main/AnimationAdditiveReferencePoseTimelineMarker.png). You can specify the reference pose by entering a frame number in the "Pose Frame" field, or by dragging the blue marker in the timeline. |
|__Mask__ |The Body mask and Transform mask applied to this animation clip (see section on [avatar masks](class-AvatarMask)).|
|__Curves__ |Parameter-related curves (see [Curves in Mecanim](animeditor-AnimationCurves)).|
|__Events__ |Used to create a new Event on a clip (see [Using Animation Events](animeditor-AnimationEvents)).|
|__Motion__ |Allows you to define a custom root motion node (see [Selecting a Root Motion Node](AnimationRootMotionNodeOnImportedClips)).|
|__Import Messages__ |Gives you information about how your animation was imported, including an optional 'Retargeting Quality Report'.|

Creating clips is essentially defining the start and end points for segments of animation. In order for these clips to loop, they should be trimmed in such a way to match the first and last frame as best as possible for the desired loop. For more on this, see the section on 
[Looping animation clips](LoopingAnimationClips)


Animation Import Warnings
-------------------------

If any problems occured during the animation import process, a warning will be displayed at the top of the Animations Import inspector, like this:

![](../uploads/Main/AnimationWarningBox.png)

The warnings do not necessarily mean your animation has not imported or will not work. It may just mean that the imported animation could look slightly different to the source animation. The detail of the warnings, if any, are displayed further down the inspector under the "Import Messages" section. The animation import warnings that you might recieve are as follows:

- Default bone length found in this file is different from the one found in the source avatar.
- Inbetween bone default rotation found in this file is different from the one found in the source avatar.
- Source avatar hierarchy doesn't match one found in this model.
- This animation has Has translation animation that will be discarded.
- Humanoid animation has inbetween transforms and rotation that will be discarded.
- Has scale animation that will be discarded.

All these messages indicate that some data present in your original file was omitted when Unity imported and converted your animation to its own internal format. These warnings essentially tell you that the retargeted animation may not exactly match the source animation.

**Note:** Pre and post-extrapolate modes (also known as pre and post-infinity modes) other than **constant** are not supported by Unity, and are converted to **constant** when imported.