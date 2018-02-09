Splitting Animations
====================


An animated character typically has a number of different movements that are activated in the game in different circumstances. These movements are called [__Animation Clips__](class-AnimationClip). For example, we might have separate animation clips for walking, running, jumping, throwing, dying, etc. Depending on the way the model was animated, these separate movements might be imported as distinct animation clips or as one single clip where each movement simply follows on from the previous one. In cases where there is only a single clip, the clip must be **split** into its component animation clips within Unity, which will involve some extra steps in your workflow.

Working with models that have pre-split animations
--------------------------------------------------


The simplest types of models to work with are those that contain pre-split animations. If you have an animation like that, the __Animations__ tab in the __Animation Importer Inspector__ will look like this:

![](../uploads/Main/MecanimImportPreSplitAnimation.png) 

You will see a list available clips which you can preview by pressing Play in the __Preview Window__ (lower down in the inspector). The frame ranges of the clips can be edited, if needed. 

Working with models that have unsplit animations
------------------------------------------------


For models where the clips are supplied as one continuous animation, the __Animation__ tab in the __Animation Importer Inspector__ will look like this:


![](../uploads/Main/MecanimImportAnimationNoSplit.png) 

In cases like this, you can define the frame ranges that correspond to each of the separate animation sequences (walking, jumping, etc). You can create a new animation clip by pressing (+) and selecting the range of frames that are included in it. 

For example:

* walk animation during frames 1 - 33
* run animation during frames 41 - 57
* kick animation during frames 81 - 97



![The Import Settings Options for Animation](../uploads/Main/MecanimImportAnimationSplitting.png) 

In the Import Settings, the __Split Animations__ table is where you tell Unity which frames in your asset file make up which Animation Clip. The names you specify here are used to activate them in your game.

For further information about the animation inspector, see the [Animation Clip component reference page](class-AnimationClip).



Animating objects and properties in Unity using Mecanim
----------------------------------------------------

You can create animation clips which animate any object or component property using Unity's animation window. These animation clips can then be arranged into a state machine in exactly the same way as external animation clips such as character animations. For example, you could animate the motion of a [camera](class-Camera), the colour of a [light](class-Light), the individual frames of a [sprite](SpriteEditor) animation, or a public property of a [script](CreatingAndUsingScripts).

To set up a Character or other GameObject for animation, you need to follow this process:

* Create a __New Animator Controller__
* Open the __Animator Window__ to edit the Animator Controller
* Drag the desired animation clip into the __Animator Controller Window__
* Drag the model asset into the Hierarchy.
* Add the animator controller to the __Animator component__ of the asset.

###Importing Animations using multiple model files

Another way to import animations is to follow a naming scheme that Unity allows for the animation files. You create separate model files and name them with the convention 'modelName@animationName.fbx'. For example, for a model called "goober", you could import separate idle, walk, jump and walljump animations using files named "goober@idle.fbx", "goober@walk.fbx", "goober@jump.fbx" and "goober@walljump.fbx". Only the animation data from these files will be used, even if the original files are exported with mesh data.


![An example of four animation files for an animated character (note that the .fbx suffix is not shown within Unity)](../uploads/Main/animation_at_naming.png) 

Unity automatically imports all four files and collects all animations to the file without the @ sign in. In the example above, the goober.mb file will be set up to reference idle, jump, walk and wallJump automatically.

For FBX files, simply export a model file with no animation ticked (eg, goober.fbx) and the 4 clips as goober@_animname_.fbx by exporting the desired keyframes for each (enable animation in the FBX dialog).

