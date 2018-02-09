Animation States
================


__Animation States__ are the basic building blocks of an __Animation State Machine__. Each state contains an individual animation sequence (or [blend tree](class-BlendTree)) which will play while the character is in that state. When an event in the game triggers a state transition, the character will be left in a new state whose animation sequence will then take over.

When you select a state in the __Animator Controller__, you will see the properties for that state in the inspector:-


![](../uploads/Main/MecanimStateInspector.png) 


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Speed__ |The default speed of the animation|
|__Motion__ |The animation clip assigned to this state|
|__Foot IK__ |Should Foot IK be respected for this state.  Applicable to humanoid animations. |
|__Write Defaults__ |Whether or not the AnimatorStates writes back the default values for properties that are not animated by its Motion. |
|__Mirror__ |Should the state be mirrored. This is only applicable to humanoid animations. |
|__Transitions__|The list of transitions originating from this state|

The default state, displayed in brown, is the state that the machine will be in when it is first activated. You can change the default state, if necessary, by right-clicking on another state and selecting __Set As Default__ from the context menu. The _solo_ and _mute_ checkboxes on each transition are used to control the behaviour of __animation previews__ - see [this page](AnimationSoloMute) for further details.

A new state can be added by right-clicking on an empty space in the __Animator Controller Window__ and selecting __Create State-&gt;Empty__ from the context menu. Alternatively, you can drag an animation into the Animator Controller Window to create a state containing that animation. (Note that you can only drag Mecanim animations into the Controller - non-Mecanim animations will be rejected.) States can also contain [Blend Trees](class-BlendTree).

###Any State
__Any State__ is a special state which is always present. It exists for the situation where you want to go to a specific state regardless of which state you are currently in. This is a shorthand way of adding the same outward transition to all states in your machine. Note that the special meaning of __Any State__ implies that it cannot be the end point of a transition (ie, jumping to "any state" cannot be used as a way to pick a random state to enter next).


![](../uploads/Main/AnyState.png) 
