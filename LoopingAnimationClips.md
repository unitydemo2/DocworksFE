Looping animation clips
=======================


A common operation for people working with animations is to make sure they loop properly. It is important, for example, that the animation clip representing the walk cycle, begins and ends in a similar pose (e.g. left foot on the ground), to ensure there is no foot sliding, or strange jerky motions. Mecanim provides convenient tools for this. Animation clips can loop based on pose, rotation, and position. 

If you drag the Start or End points of the animation clip, you will see the Looping fitness curves for all of the paramers based on which it is possible to loop. If you place the Start / End marker in a place where the curve for the property is green, it is more likely that the clip can loop properly. The __loop match__ indicator will show how good the looping is for the selected ranges. 


![Clip ranges with bad match for __Loop Pose__](../uploads/Main/MecanimAnimClipLoopingRed.png) 

![Clip ranges with good match for __Loop Pose__](../uploads/Main/MecanimAnimClipLoopingGreen.png) 

Once the __loop match__ indicator is green, Enabling __Loop Pose__ (for example) will make sure the looping of the pose is artifact-free. 

For more details on animation clip options, see [Animation Clip reference](class-AnimationClip).

