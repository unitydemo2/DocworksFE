#Creating the Avatar

After a model file (FBX, COLLADA, etc.) is imported, you can specify what kind of rig it is in the __Rig__ tab of the __ModelImporter options__. 



##Humanoid animations

For a Humanoid rig, select __Humanoid__ and click __Apply__. Mecanim will attempt to match up your existing bone structure to the Avatar bone structure. In many cases, it can do this automatically by analysing the connections between bones in the rig.

If the match has succeeded, you will see a check mark next to the __Configure__ menu

![](../uploads/Main/MecanimImporterRigTab.png) 

Also, in the case of a successful match, an Avatar sub-asset is added to the model asset, which you will be able to see in the project view hierarchy. 

![Models with and without an Avatar sub-asset](../uploads/Main/MecanimFBXNoAvatar.png) 


![The inspector for an Avatar asset](../uploads/Main/MecanimAvatarCreated.png) 

If Mecanim was unable to create the Avatar, you will see a cross next to the __Configure__ button, and no Avatar sub-asset will be added. When this happens, you need to [configure the avatar manually](ConfiguringtheAvatar).


##Non-humanoid animations

Two options for non-humanoid animation are provided: _Generic_ and _Legacy_. Generic animations are imported using the Mecanim system but don't take advantage of the extra features available for humanoid animations. Legacy animations use the the animation system that was provided by Unity before Mecanim. There are some cases where it is still useful to work with legacy animations (most notably with legacy projects that you don't want to update fully) but they are seldom needed for new projects. See [this section](Animations) of the manual for further details on legacy animations.
