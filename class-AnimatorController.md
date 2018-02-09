Animator Controller
===================

An Animator Controller asset is created within Unity and allows you to arrange and maintain a set of animations for a character or object. In most situations, it is normal to have multiple animations and switch between them when certain game conditions occur. For example, you could switch from a walk animation to a jump whenever the spacebar is pressed.  However even if you just have a single animation clip you still need to place it into an animator controller to use it on a Game Object. 

The controller has references to the animation clips used within it, and manages the various animation states and the transitions between them using a so-called __State Machine__, which could be thought of as a kind of flow-chart, or a simple program written in a visual programming language within Unity. More information about state machines can be found [here](AnimationStateMachines).

![A simple Animator Controller](../uploads/Main/MecanimAnimatorControllerWindow.png)

In some situations, an Animator Controller is automatically created for you, such as in the situation where you begin animating a new GameObject using the Animation Window.

In other cases, you would want to create a new Animator Controller asset yourself and begin to add states to it by dragging in animation clips and creating transitions between them to form a state machine.