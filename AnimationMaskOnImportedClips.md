Masking Imported Clips
===================================================

Masking allows you to discard some of the animation data within a clip, allowing the clip to animate only parts of the object or character rather than the entire thing.  A good example of this would be a character with a throwing animation. If you wanted to be able to use the throwing animation in conjunction with various other body movements such as running, crouching and jumping, you could create a mask for the throwing animation limiting it to just the right arm, upper body and head. This portion of the animation can then be played in a layer over the top of the base running or jumping animations.

Masking can be applied to animation clips either during import time, or at runtime. Masking during import time is preferable, because it allows the discarded animation data to be omitted from your build, making filesize and memory footprint smaller. It also makes for faster processing speed because there is less animation data to be blended at runtime. In some cases, import masking may not be suitable for your purposes, in which case you can apply a mask at runtime by using the layer settings of the Animator Controller. This page relates to masking in the import settings.

To apply a mask to an imported animation clip, first select the imported animation file in your project view, then in the import settings in the inspector, select the Animations button.

![View the Animations section of the Import Settings for your animation file](../uploads/Main/FBXImporterInspectorAnimationsSection.png) 

Then scroll all the way to the bottom of the inspector to find the Mask heading, among the four fold-out headings as shown:

![The Motion fold-out heading, along with the Curves, Events and Motion headings](../uploads/Main/AnimationInspectorMasksCurvesEventsMotion.png) 

Expand the Mask heading to reveal the Mask options. When you open the menu, you'll see three options: Definition, Humanoid and Transform.

![The Mask Definition, Humanoid and Transform options](../uploads/Main/AnimationInspectorMaskOptions.png) 

Definition
----------
Allows you to specify whether you want to create a one-off mask in the inspector specially for this clip, or whether you want to use an existing mask asset from your project. 

If you want to create a one-off mask just for this clip, choose / Create From This Model /.

If you are going to set up multiple clips with the same mask, you should select / Copy From Other Mask / and use a mask asset. This allows you to re-use a single mask definition for many clips.

When Copy From Other Mask is selected, the Humanoid and Transform options are unavailable, since these relate to creating a one-off mask within the inspector for this clip.

![Here, the Copy From Other option is selected, and a Mask asset has been assigned](../uploads/Main/AnimationInspectorMaskCopyFromOther.png) 


Humanoid
--------

The Humanoid option gives you a quick way of defining a mask by selecting or deselecting the body parts of a human diagram. These can be used if the animation has been marked as humanoid and has a valid avatar.

![The Humanoid mask selection option](../uploads/Main/AnimationInspectorMaskHumanoidSelection.png) 


Transform
---------

This option allows you to specify a mask based on the individual bones or moving parts of the animation. This gives you finer control over the exact mask definition, and also allows you to apply masks to non-humanoid animation clips.

![The Humanoid mask selection option](../uploads/Main/AnimationInspectorMaskTransformSelection.png) 

