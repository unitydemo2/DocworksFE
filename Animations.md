Legacy Animation System
=======================


Prior to the introduction of Mecanim, Unity used a simpler animation system. For backward compatibility, this system is still available. The main reason for using legacy animation is to continue working with an old project without the work of updating it for Mecanim. However, it is not recommended that you use the legacy system for new projects.

Working with legacy animations
------------------------------


To import a legacy animation, you first need to mark it as such in the Mesh importer's Rig tab:

![](../uploads/Main/MecanimLegacyRigTab.png)

The Animation tab on the importer will then look something like this:

![](../uploads/Main/MecanimLegacyAnimationProps.png)

| | |
|:---|:---|
|__Import Animation__ |Selects whether or not animation should be imported at all. |
|__Wrap Mode__ |The method of handling what happens when the animation comes to an end:- |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Default__ |Uses whatever setting is specified in the animation clip. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Once__ |Play the clip to the end and then finish. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Loop__ |Play to the end, then immediately restart from the beginning. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__PingPong__ |Play to the end, then play from the end in reverse, and so on. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Forever__ |Play to the end, then loop the last frame indefinitely. |
|__Anim Compression__ |Settings to attempt to remove redundant information from clips. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Off__ |No compression. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Keyframe reduction__ |Attempt to remove keyframes where differences are too small to be seen|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Keyframe reduction and compression__|As for _Keyframe reduction_, but clip data is also compressed. |
|__Rotation error__ |Minimum difference in rotation values (in degrees), below which two keyframes are counted as equal. |
|__Position error__ |Minimum difference in position (as a percentage of coordinate values), below which two keyframes are counted as equal. |
|__Rotation error__ |Minimum difference in scale (as a percentage of coordinate values), below which two keyframes are counted as equal. |


Below the properties in the inspector is a list of animation clips. When you click on a clip in the list, an additional panel will appear below it in the inspector:-


![](../uploads/Main/MecanimLegacyAnimationClips.png) 

The Start and End values can be changed to allow you to use just a part of the original clip (see the page on [|splitting animations](Splittinganimations) for further details). The _Add Loop Frame_ option adds an extra keyframe to the end of the animation that is exactly the same as the keyframe at the start. This enables the animation to loop smoothly even when the last frame doesn't exactly match up with the first. The _Wrap Mode_ setting is identical to the master setting in the main animation properties but applies only to that specific clip.
