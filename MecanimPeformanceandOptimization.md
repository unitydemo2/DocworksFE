Performance and Optimization
====================================


This page contains some tips to help you obtain the best performance from [Mecanim](AnimationOverview), covering character setup, the animation system and runtime optimizations.

Character Setup
---------------


###Number of Bones
In some cases you will need to create characters with a large number of bones, for example when you want a lot of customizable attachments. These extra bones will increase the size of the build, and you could expect to have a relative processing cost for each additional bone. For example, 15 additional bones on a rig that already has 30 bones will take 50% longer to solve in __Generic__ mode. Note that you can have additional bones in [Generic](GenericAnimations) and in [Humanoid](AvatarCreationandSetup) mode. When you have no animations playing using the additional bones, the processing cost should be negligible. This cost will be even lower if their attachments are non existent or hidden.

###Multiple Skinned Meshes
Combine skinned meshes whenever possible. Splitting a character into two [Skinned Mesh Renderers](class-SkinnedMeshRenderer) is a bad idea with regard to performance. It's better if your character has just one material, but there are some cases when you might require more materials.

Animation System
----------------


###Controllers
The [Animator](class-Animator) doesn't spend time processing when a [Controller](class-AnimatorController) is not set to it.

###Simple Animation
Playing a single [Animation Clip](class-AnimationClip) with no blending can make Mecanim slower than the [legacy animation system](Animations). The old system is very direct, sampling the curve and directly writing into the transform. Mecanim has temporary buffers it uses for blending, and there is additional copying of the sampled curve and other data. The Mecanim layout is optimized for animation blending and more complex setups.

###Scale Curves
Animating scale curves is more expensive than animating translation and rotation curves. To improve performance, avoid scale animations.  

**Note:** This does not apply to constant curves (curves that have the same value for the length of the [Animation Clip](class-AnimationClip) ). Constant curves are optimized, and are less expensive that normal curves. Constant curves that have the same values as the default scene values will not write to the scene every frame.

###Layers
Most of the time Mecanim is evaluating animations, and the overhead for [AnimationLayers](AnimationLayers) and [AnimationStateMachines](AnimationStateMachines) is kept to the minimum. The cost of adding another layer to the animator, synchronized or not, depends on what animations and blend trees are played by the layer. When the weight of the layer is zero, the layer update will be skipped.

###Humanoid vs. Generic Modes
These tips will help you decide between these modes:


* When importing Humanoid animation use a BodyMask to remove IK Goals or fingers animation if they are not needed.
* When you use Generic, using root motion is more expensive than not using it. If your animations don't use root motion, make sure that you have no root bone selected.

###Mecanim Scene
There are many optimizations that can be made, some useful tips include:


* Use hashes instead of strings to query the Animator.
* Implement a small AI Layer to control the Animator. You can make it provide simple callbacks for OnStateChange, OnTransitionBegin, etc.
* Use State Tags to easily match your AI state machine to the Mecanim state machine.
* Use additional curves to simulate Events.
* Use additional curves to mark up your animations, for example in conjunction with [target matching](TargetMatching).

Runtime Optimizations
---------------------


###Visibility and Updates
Always optimize animations by setting the animators's Culling Mode to Based on Renderers, and disable the skinned mesh renderer's Update When Offscreen property. This way animations won't be updated when the character is not visible. See the [skinned mesh renderer](class-SkinnedMeshRenderer) for further information.

---
<span class="page-edit">• 2017-05-16  <!-- include IncludeTextAmendPageNoEdit --></span><br/>
