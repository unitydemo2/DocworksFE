FBX Importer, Rig options
=========================


The Rig tab allows you to assign or create an avatar definition to your imported skinned model so that you can animate it - see [Asset Preparation and Import](AssetPreparationandImport)

If you have a **humanoid character** (ie, two legs, two arms and a head) then choose Humanoid and 'Create from this model'. An Avatar will be created to best match the bone hierarchy - see [Avatar Creation and Setup](AvatarCreationandSetup) or you can pick an alternative avatar Definition that has already been set up.

If you have a non humanoid character e.g. a quadruped, or any animatable entity that you wish to use with [Mecanim](AnimationOverview) choose **Generic**. After choosing you will then need to identify a bone in the drop down to use as the 
root node.

Choose legacy if you wish to use the legacy animation system and import and use animations as with 3.x


![](../uploads/Main/MecanimImporterRigTab.png) 


|**_Property:_** ||**_Function:_** |
|:---|:---|:---|
|__Animation Type__ ||The type of animation.|
||__None__|No animation present|
||__Legacy__|Legacy animation system|
||__Generic__|Generic Mecanim animation|
||__Humanoid__|Humanoid Mecanim animation system|
|__Avatar Definition__||Where to get the Avatar definition|
||__Create from this model__|The Avatar should be based on this model|
||__Copy from other Avatar__|Point to an Avatar config set up on another model. |
|__Configure...__||Go to the [Avatar configuration](ConfiguringtheAvatar)|
|__Optimize Game Object__||When turned on, the game object transform hierarchy of the imported character will be removed and stored in the Avatar and Animator component. The SkinnedMeshRenderers of the character will then directly use the Mecanim internal skeleton. This option improves the performance of the animated characters. You should turn it on for the final product. In optimized mode skinned mesh matrix extraction is also multithreaded. |
