#Muscle setup

Mecanim allows you to control the range of motion of different bones using __Muscles__. 

Once the Avatar has been [properly configured](ConfiguringtheAvatar), Mecanim will "understand" the bone structure and allow you to start working in the __Muscles__ tab of the __Avatar Inspector__. Here, it is very easy to tweak the character's range of motion and ensure the character deforms in a convincing way, free from visual artifacts or self-overlaps.

![](../uploads/Main/MecanimAvatarMuscles.png) 

You can either adjust individual bones in the body (lower part of the view) or manipulate the character using predefined deformations which operate on several bones at once (upper part of the view).

The "Translate DoF" option shown at the bottom of the Additional Settings section allows you to enable the use of translation animations for the humanoid. With this option disabled, the bones are animated using only rotations. You would only want to enable this option if you know your animation contains animated tranlations of some of the bones in your character. Enabling translation DoF comes with some performance cost as the animation system needs to do an extra step to retarget humanoid animation. Translation DoF is available for Chest, UpperChest, Neck, LeftUpperLeg, RightUpperLeg, LeftShoulder and RightShoulder muscles.