# Animation transitions

Animation transitions allow the [state machine](StateMachineBasics) to switch or blend from one animation state to another. Transitions define not only how long the blend between states should take, but also under what conditions they should activate. You can set up a transition to occur only when certain conditions are true. To set up these conditions, specify values of parameters in the Animator Controller.

For example, your character might have a "patrolling" state and a "sleeping" state. You could set the transition between patrolling and sleeping to occur only when an "alertness" parameter value drops below a certain level.

![An example of a transition as viewed in the inspector.](../uploads/Main/classTransitionAnimatorPreview.png)

To give transitions a name, type it into the field as shown below:

![](../uploads/Main/AnimatorTransitionName.png)

The Inspector window of a state shows the transitions the state uses as shown below:

![](../uploads/Main/AnimatorTransitionNameInState.png)

There can be only one transition active at any given time. However, the currently active transition can be interrupted by another transition if you have configured the settings to allow it (see [Transition Interruption](#TransitionInterruption) below).

### Transition properties

To view properties for a transition, click on the transition line connecting two states in the Animator window. The properties appear in the Inspector window.

![](../uploads/Main/class-Transition-Properties.png)

Use the following properties to adjust the transition and how it blends between the current and next state.

| **Property**| **Function** |
|:---|:---| 
| __Has Exit Time__|  __Exit Time__ is a special transition that doesn’t rely on a parameter. Instead, it relies on the normalized time of the state. Check to make the transition happen at the specific time specified in __Exit Time__. |
| __Settings__| Fold-out menu containing detailed transition settings as below. |
| __Exit Time__| If __Has Exit Time__ is checked, this value represents the exact time at which the transition can take effect. This is represented in normalized time (for example, an exit time of 0.75 means that on the first frame where 75% of the animation has played, the __Exit Time__ condition is true). On the next frame, the condition is false.<br/><br/>For looped animations, transitions with exit times smaller than 1 are evaluated every loop, so you can use this to time your transition with the proper timing in the animation every loop. <br/><br/>Transitions with an __Exit Time__ greater than 1 are evaluated only once, so they can be used to exit at a specific time after a fixed number of loops. For example, a transition with an exit time of 3.5 are evaluated once, after three and a half loops. |
| __Fixed Duration__| If the __Fixed Duration__ box is checked, the transition time is interpreted in seconds. If the __Fixed Duration__ box is not checked, the transition time is interpreted as a fraction of the normalized time of the source state. |
| __Transition Duration__| The duration of the transition, in normalized time or seconds depending on the __Fixed Duration__ mode, relative to the current state’s duration. This is visualized in the transition graph as the portion between the two blue markers.|
| __Transition Offset__| The offset of the time to begin playing in the destination state which is transitioned to. For example, a value of 0.5 means the target state begins playing at 50% of the way through its own timeline. |
| __Interruption Source__| Use this to control the circumstances under which this transition may be interrupted (see [Transition interruption](#TransitionInterruption) below). |
| __Ordered Interruption__| Determines whether the current transition can be interrupted by other transitions independently of their order (see [Transition interruption](#TransitionInterruption) below).|
| __Conditions__| A transition can have a single condition, multiple conditions, or no conditions at all. If your transition has no conditions, the Unity Editor only considers the __Exit Time__, and the transition occurs when the exit time is reached. If your transition has one or more conditions, the conditions must all be met before the transition is triggered.<br/><br/>A condition consists of: <br/><br/>- An event parameter (the value considered in the condition). <br/>- A conditional predicate (if needed,for example, ‘less than’ or ‘greater than’ for floats). <br/>- A parameter value (if needed). <br/><br/>If you have __Has Exit Time__ selected for the transition and have one or more conditions, note that the Unity Editor considers whether the conditions are true after the __Exit Time__. This allows you to ensure that your transition occurs during a certain portion of the animation. |

<a name="TransitionInterruption"></a>

### Transition interruption

Use the  __Interruption Source__ and __Ordered Interruption__ properties  to control how your transition can be interrupted.

The interruption order works, conceptually, as if transitions are queued and then parsed for a valid transition from the first transition inserted to the last.

#### Interruption Source property

The transitions in [AnyState](class-State) are always added first in the queue, then other transitions are queued depending on the value of __Interruption Source__:

| **Value**| **Function** |
|:---|:---| 
| __None__| Don’t add any more transitions. |
| __Current State__| Queue the transitions from the current state. |
| __Next State__| Queue the transitions from the next state. |
| __Current State then Next State__| Queue the transitions from the current state, then queue the ones from the next state. |
| __Next State then Current State__| Queue the transitions from the next state, then queue the ones from the current state. |

**Note**: This means that even with the __Interruption Source__ set to __None__, transitions can be interrupted by one of the  [AnyState](class-State) transitions.

#### Ordered Interruption property

The property __Ordered Interruption__ changes how the queue is parsed.

Depending on its value, parsing the queue ends at a different moment as listed below.

| **Value**| **Ends when** |
|:---|:---| 
| __Checked__| A valid transition or the current transition has been found. |
| __Unchecked__| A valid transition has been found. |

Only an [AnyState](class-State) transition can be interrupted by itself.

To learn more about transition interruptions, see the Unity blog post [State Machine Transition Interruptions](https://blogs.unity3d.com/2016/07/13/wait-ive-changed-my-mind-state-machine-transition-interruptions/).

### Transition graph

To manually adjust the settings listed above, you can either enter numbers directly into the fields or use the transition graph. The transition graph modifies the values above when the visual elements are manipulated.

![The Transition settings and graph as shown in the Inspector](../uploads/Main/AnimatorTransitionSettingsAndGraph.svg)

Change the transition properties in the graph view using the following directions::

* Drag the __Duration "out"__ marker to change the __Duration__ of the transition.
* Drag the __Duration "in"__ marker to change the duration of the transition and the __Exit Time__.
* Drag the target transition to adjust the __Transition Offset__.
* Drag the preview playback marker to scrub through the animation blend in the preview window at the bottom of the Inspector.

### Transitions between Blend Tree states

If either the current or next state belonging to this transition is a [Blend Tree](class-BlendTree) state, the Blend Tree parameters appear in the Inspector. Adjust these values to preview how your transition would look with the Blend Tree values set to different configurations. 
If your Blend Tree contains clips of differing lengths, you should test what your transition looks like when showing both the short clip and the long clip. Adjusting these values does not affect how the transition behaves at runtime; they are solely for helping you preview how the transition could look in different situations.

![The Blend Tree parameter preview controls, visible when either your current or next state is a Blend Tree state.](../uploads/Main/AnimatorTransitionInspectorShowingBlendtreeParams.png)

<a name="Conditions"></a>

###Conditions

A transition can have a single condition, multiple conditions, or no conditions at all. If your transition has no conditions, the Unity Editor only considers the __Exit Time__, and the transition occurs when the exit time is reached. If your transition has one or more conditions, the conditions must all be met before the transition is triggered.

A condition consists of:

* An event parameter, the value of which is considered in the condition.
* A conditional predicate, if needed (for example, less or greater for floats).
* A parameter value, if needed.

If __Has Exit Time__ is enabled for the transition and has one or more conditions, these conditions are only checked after the exit time of the state. This allows you to ensure that your transition only occurs during a certain portion of the animation.