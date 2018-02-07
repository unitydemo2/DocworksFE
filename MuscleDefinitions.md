#Muscle setup

Unity's animation system allows you to control the range of motion of different bones using __Muscles__. 

Once the Avatar has been [properly configured](ConfiguringtheAvatar), the animation system "understands" the bone structure and allows you to start using the __Muscles & Settings__ tab of the __Avatar__'s Inspector. Use the __Muscles & Settings__ tab to tweak the character's range of motion and ensure the character deforms in a convincing way, free from visual artifacts or self-overlaps.

![](../uploads/Main/MecanimAvatarMuscles.png) 

Use the __Muscle Group Preview__ to manipulate the character using predefined deformations. These affect several bones at once. Use the __Per-Muscle Settings__ and __Additional Settings__ to adjust individual bones in the body.

## Translate Degree of Freedom (DoF)

In the __Additional Settings__, tick the __Translate DoF__ option if you want to enable translation animations for the humanoid. If the checkbox is unticked, Unity animates the bones using only rotations. __Translation DoF__ is available for Chest, UpperChest, Neck, LeftUpperLeg, RightUpperLeg, LeftShoulder and RightShoulder muscles.

Enabling __Translate DoF__ can increase performance requirements, because the animation system needs to do an extra step to retarget humanoid animation. For this reason, you should only enable this option if you know your animation contains animated translations of some of the bones in your character.