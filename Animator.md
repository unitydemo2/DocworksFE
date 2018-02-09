The Animator Controller Asset
================================

When you have an animation clips ready to use, you need to use an __Animator Controller__ to bring them together. An Animator Controller asset is created within Unity and allows you to maintain a set of animations for a character or object.

![An Animator Controller Asset in the Project Folder](../uploads/Main/AnimatorAssetIcon.png)

Animator Controller assets are created from the Assets menu, or from the Create menu in the Project window.

In most situations, it is normal to have multiple animations and switch between them when certain game conditions occur. For example, you could switch from a walk animation to a jump whenever the spacebar is pressed.  However even if you just have a single animation clip you still need to place it into an animator controller to use it on a Game Object. 

The controller manages the various animation states and the transitions between them using a so-called __State Machine__, which could be thought of as a kind of flow-chart, or a simple program written in a visual programming language within Unity. More information about state machines can be found [here](AnimationStateMachines). The structure of the Animator Controller can be created, viewed and modified in the [Animator Window](Manual:AnimatorWindow).

![A simple Animator Controller](../uploads/Main/MecanimAnimatorControllerWindow.png)

The animator controller is finally applied to an object by attaching an __Animator__ component that references them. See the reference manual pages about the [Animator](class-Animator) component and [Animator Controller](class-AnimatorController) for further details about their use.


