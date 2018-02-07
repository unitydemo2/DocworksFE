# Non-humanoid Animations

The full power of Unity's Animation system is most evident when you are working with humanoid Animations. However, non-humanoid animations are also supported although without the avatar system and other humanoid-specific features. Non-humanoid animations are referred to as __Generic Animations__.

To start working with a generic skeleton, go to the Rig tab in the FBX importer and choose __Generic__ from the Animation Type menu.


![](../uploads/Main/MecanimImportRigGeneric.png) 

## Root node in generic animations

When working wth humanoid animations, Unity can determine the center of mass and orientation of the rig. When working with Generic animations, the skeleton can be arbitrary, so you must specify which bone is the __Root node__. The __Root node__ allows Unity to establish consistency between Animation clips for a generic model, and blend properly between Animations that have not been authored "in place" (that is, where the whole model moves its world position while animating).

Specifying the root node also allows Unity to determine between movement of the bones relative to each other, and motion of the __Root node__ in the world (controlled from [OnAnimatorMove](ScriptRef:MonoBehaviour.OnAnimatorMove.html)).
