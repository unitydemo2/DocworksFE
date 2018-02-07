# Animation Preview

Use the Animation Preview to visualize your Animation clips on a 3D [Model](FBXImporter-Model) or a 2D [Sprite](Sprites).

To access the Animation Preview, navigate to the Project window and select your [Animation clip](https://docs.unity3d.com/Manual/class-AnimationClip.html). The Animation Preview appears at the bottom of the Inspector window. Drag a Model or Sprite into the Preview area to see how it looks with your [Animation clip](class-AnimationClip).

![The Animation Preview at the bottom of the Inspector window](../uploads/Main/AnimationPreview-Preview.png)

You can also use the Preview window to view the Animation from an [Animator Controller](class-AnimatorController). To do this, create a [transition](StateMachineTransitions) arrow between two [states](class-State) in your Animator Controller, and click on one of the transition arrows. The Animation Preview appears at the bottom of the Inspector window. Press the Play button in the Preview to show the transition between the two states.

## Using the Animation Preview

Click and drag around the Preview window with your mouse to pan around. Use your scroll wheel to zoom in and out. This follows the [root](RootMotion) of your Animation so that your Model or Sprite doesn’t move out of sight within the Preview area. 

The following sections describe the user interface of the Animation Preview, from left to right. 

### Play

Click the Play icon to view your Animation on your Model or Sprite. 

Click and drag the white line in the timeline at the top of the Preview to cycle through the frames in your Animation clip.

![](../uploads/Main/AnimationPreview-Play.png)

### 2D view mode

Use the 2D view mode to view your animations on a 2D plane. The __2D__ button toggles the 2D mode on and off. 

![The _2D_ button. In this image, 2D view mode is enabled.](../uploads/Main/AnimationPreview-2DView.png)

Unity enables this mode by default when you create or use a 2D Project, but you can use it in both 2D and 3D Projects. 

To switch from 2D to 3D view mode, click the 2D button, or right-click and drag around the Preview space with your mouse to orbit the view. 

### Gizmo visibility

Click the Gizmo Visibility button (the button with three arrows) to toggle the visibility of the [gizmos](GizmosMenu) in the Preview window.

![The Gizmo Visibility button. In this image, Gizmo Visibility is enabled.](../uploads/Main/AnimationPreview-Gizmo.png)

The Preview gizmos provide visual feedback on the Asset's [center of mass](https://en.wikipedia.org/wiki/Center_of_mass) and root motion.

### Animation speed

Use the slider at the top of the Preview to change how fast the Animation preview plays. 

![](../uploads/Main/AnimationPreview-Slider.png)

## Avatar

Click the Avatar icon in the bottom-right of the panel to open a drop-down list of available avatar Models. Select an avatar Model to use in the Preview window. 

![](../uploads/Main/AnimationPreviewAvatar.png)

## Humanoid preview

Unity provides a built-in humanoid Model to allow you to preview humanoid Animation files even before you import your own Models. To use this, navigate to the Project window, click on the Animation file, and click __Rig__ in the Inspector window. Set the __Animation Type __to __Humanoid__.


![](../uploads/Main/AnimationPreview-Humanoid.png)

Return to the __Animation__ tab. By default, Unity uses the built-in humanoid Model in the Preview.

![](../uploads/Main/AnimationPreview-Humanoid2.png)

If you have your own humanoid-configured Model, drag and drop it from the Scene or Project window to the Preview to see the Animation clip on that Model.

#### IK

The __IK__ button is only visible when you are previewing a humanoid Model. Click the __IK__ button to force the feet of your Preview Model to reach the Foot position of your Animation’s source skeleton. This prevents any unintended behaviour that might occur because of the differences in proportion between your Model and your Animation’s skeleton. See documentation on [Inverse Kinematics](InverseKinematics) for more information.

This is similar to enabling __Foot IK__ on a state in an Animator Controller.  

![](../uploads/Main/AnimationPreview-FootIK.png)

---

* <span class="page-history">2D view mode new feature in Unity 2017.3</span>

* <span class="page-edit"> 2017-11-29  <!-- include IncludeTextAmendPageSomeEdit --></span>