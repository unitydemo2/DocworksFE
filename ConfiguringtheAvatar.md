#Configuring the Avatar



Since the __Avatar__ is such an important aspect of the Mecanim system, it is important that it is configured properly for your model. So, whether the [automatic Avatar creation](class-Avatar) fails or succeeds, you need to go into the __Configure Avatar__ mode to ensure your Avatar is valid and properly set up. It is important that your character's bone structure matches Mecanim's predefined bone structure _and_ that the model is in T-pose.

If the automatic Avatar creation fails, you will see a cross next to the _Configure_ button. 

![](../uploads/Main/MecanimAvatarInvalid.png) 

If it succeeds, you will see a check/tick mark:

![](../uploads/Main/MecanimAvatarApplied.png) 

Here, success simply means all of the required bones have been matched but for better results, you might want to match the optional bones as well and get the model into a proper T-pose.

When you go to the __Configure ...__ menu, the editor will ask you to save your scene. The reason for this is that in __Configure__ mode, the Scene View is used to display bone, muscle and animation information for the selected model alone, without displaying the rest of the scene.


![](../uploads/Main/MecanimConfigureAvatarSaveDialog.png) 

Once you have saved the scene, you will see a new __Avatar Configuration__ inspector, with a bone mapping.

![](../uploads/Main/MecanimAvatarMappingValid.png) 

The inspector shows which of the bones are required and which are optional - the optional ones can have their movements interpolated automatically. For Mecanim to produce a valid match, your skeleton needs to have at least the required bones in place. In order to improve your chances for finding a match to the Avatar, name your bones in a way that reflects the body parts they represent (names like "LeftArm", "RightForearm" are suitable here). 

If the model does NOT yield a valid match, you can manually follow a similar process to the one used internally by Mecanim:- 


1. __Sample Bind-pose__ (try to get the model closer to the pose with which it was modelled, a sensible initial pose)
1. __Automap__ (create a bone-mapping from an initial pose)
1. __Enforce T-pose__ (force the model closer to T-pose, which is the default pose used by Mecanim animations)


![](../uploads/Main/MecanimPoseMenus.png) 

If the auto-mapping (__Mapping-&gt;Automap__) fails completely or partially, you can assign bones by either draging them from the __Scene__ or from the __Hierarchy__. If Mecanim thinks a bone fits, it will show up as green in the __Avatar Inspector__, otherwise it shows up in red. 

Finally, if the bone assignment is correct, but the character is not in the correct _pose_, you will see the message "Character not in T-Pose". You can try to fix that with __Enforce T-Pose__ or rotate the remaining bones into T-pose. 


![](../uploads/Main/MecanimMappingMenus.png) 


##Avatar Body Masks

Sometimes it is useful to restrict an animation to specific body parts. For example, an walking animation might involve the character swaying their arms, but if they pick up a torch, they should hold it up to cast light. You can use an __Avatar Body Mask__ to specify which parts of a character an animation should be restricted to. See documentation on [Avatar Masks](class-AvatarMask) for further details.

