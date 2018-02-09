# Rigidbody 2D

A Rigidbody 2D component places an object under the control of the physics engine. Many concepts familiar from the standard [Rigidbody](http://docs.unity3d.com/Manual/class-Rigidbody.html) component carry over to Rigidbody 2D; the differences are that in 2D, objects can only move in the XY plane and can only rotate on an axis perpendicular to that plane.

![The Rigidbody 2D component. This appears differently in the Unity Editor depending on which Body Type you have selected. See [Body Type](#BodyType), below, to learn more.](../uploads/Main/Rigidbody2D.png)

## How a Rigidbody 2D works

Usually, the Unity Editor’s Transform component defines how a GameObject (and its child GameObjects) is positioned, rotated and scaled within the Scene. When it is changed, it updates other components, which may update things like where they render or where colliders are positioned. The 2D physics engine is able to move colliders and make them interact with each other, so a method is required for the physics engine to communicate this movement of colliders back to the Transform components. This movement and connection with colliders is what a Rigidbody 2D component is for. 

The Rigidbody 2D component overrides the Transform and updates it to a position/rotation defined by the Rigidbody 2D. Note that while you can still override the Rigidbody 2D by modifying the Transform component yourself (because Unity exposes all properties on all components), doing so will cause problems such as GameObjects passing through or into each other, and unpredictable movement.

Any Collider 2D component added to the same GameObject or child GameObject is implicitly attached to that Rigidbody 2D. When a Collider 2D is attached to the Rigidbody 2D, it moves with it. A Collider 2D should never be moved directly using the Transform or any collider offset; the Rigidbody 2D should be moved instead. This offers the best performance and ensures correct collision detection. Collider 2Ds attached to the same Rigidbody 2D won’t collide with each other. This means you can create a set of colliders that act effectively as a single compound collider, all moving and rotating in sync with the Rigidbody 2D.

When designing a Scene, you are free to use a default Rigidbody 2D and start attaching colliders. These colliders allow any other colliders attached to different Rigidbody 2Ds to collide with each other.

###Tip

Adding a __Rigidbody 2D__ allows a sprite to move in a physically convincing way by applying forces from the scripting API. When the appropriate collider component is also attached to the sprite GameObject, it is affected by collisions with other moving GameObjects. Using physics simplifies many common gameplay mechanics and allows for realistic behavior with minimal coding.

<a name="BodyType"></a>
## Body Type

The Rigidbody 2D component has a setting at the top labelled __Body Type__. The option you choose for this affects the other settings available on the component.

![](../uploads/Main/Rigidbody2DBodyType.png)


There are three options for __Body Type__; each defines a common and fixed behavior. Any Collider 2D attached to a Rigidbody 2D inherits the Rigidbody 2D’s __Body Type__. The three options are:

* __Dynamic__
* __Kinematic__
* __Static__

The option you choose defines:

* Movement (position & rotation) behavior
* Collider interaction

Note that although Rigidbody 2Ds are often described as colliding with each other, it is the  Collider 2Ds attached to each of those bodies which collide. Rigidbody 2Ds cannot collide with each other without colliders.

Changing the Body Type of a Rigidbody 2D can be a tricky process. When a Body Type changes, various mass-related internal properties are recalculated immediately, and all existing contacts for the Collider 2Ds attached to the Rigidbody 2D need to be re-evaluated during the GameObject’s next [FixedUpdate](ScriptRef:MonoBehaviour.FixedUpdate.html). Depending on how many contacts and Collider 2Ds are attached to the body, changing the Body Type can cause variations in performance.  

### Body Type: Dynamic

![](../uploads/Main/Rigidbody2D_Dynamic.png)

A __Dynamic__ Rigidbody 2D is designed to move under simulation. It has the full set of properties available to it such as finite mass and drag, and is affected by gravity and forces. A Dynamic body will collide with every other body type, and is the most interactive of body types. This is the default body type for a Rigidbody 2D, because it is the most common body type for things that need to move. It’s also the most performance-expensive body type, because of its dynamic nature and interactivity with everything around it. All Rigidbody 2D properties are available with this body type.

Do not use the Transform component to set the position or rotation of a __Dynamic__  Rigidbody 2D. The simulation repositions a __Dynamic__ Rigidbody 2D according to its velocity; you can change this directly via forces applied to it by scripts, or indirectly via collisions and gravity.

|**Property:** |**Function:** |
|:---|:---|
| __Body Type__ |Set the RigidBody 2D’s component settings, so that you can manipulate movement (position and rotation) behavior and Collider 2D interaction. <br/>Options are: __Dynamic__, __Kinematic__, __Static__ |
| __Material__ |Use this to specify a common material for all Collider 2Ds attached to a specific parent Rigidbody 2D. <br/>**Note:** A Collider 2D uses its own Material property if it has one set. If there is no Material specified here or in the Collider 2D, the default option is __None (Physics Material 2D)__. This uses a default Material which you can set in the [Physics 2D Settings](class-Physics2DManager) window. <br/>A Collider 2D uses the following order of priority to determine which __Material__ setting to use: <br/>1. A Physics Material 2D specified on the Collider 2D itself.<br/> 2. A Physics Material 2D specified on the attached Rigidbody 2D.<br/> A Physics Material 2D default material specified in the [Physics 2D Settings](class-Physics2DManager).<br/> **TIP:** Use this to ensure that all Collider 2Ds attached to the same __Static__ Body Type Rigidbody 2D can all use the same Material. |
| __Simulated__ |Enable __Simulated__ (check the box) if you want the Rigidbody 2D and any attached Collider 2Ds and Joint 2Ds to interact with the physics simulation during run time. If this is disabled (the box is unchecked), these components do not interact with the simulation. See [Rigidbody 2D properties: Simulated](#SimulatedProperty), below, for more details. This box is checked by default. |
| __Use Auto Mass__ |Check the box if you want the Rigidbody 2D to automatically detect the GameObject’s mass from its Collider 2D. |
| __Mass__ |Define the mass of the Rigidbody 2D. This is grayed out if you have selected Use Auto Mass. |
| __Linear Drag__ |Drag coefficient affecting positional movement. |
| __Angular Drag__ |Drag coefficient affecting rotational movement. |
| __Gravity Scale__ |Define the degree to which the GameObject is affected by gravity. |
| __Collision Detection__ |Define how collisions between Collider 2D are detected. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Discrete | When you set the __Collision Detection__ to __Discrete__, GameObjects with Rigidbody 2Ds and Collider 2Ds can overlap or pass through each other during a physics update, if they are moving fast enough. Collision contacts are only generated at the new position.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Continuous | When the __Collision Detection__ is set to __Continuous__, GameObjects with Rigidbody 2Ds and Collider 2Ds do not pass through each other during an update. Instead, Unity calculates the first impact point of any of the Collider 2Ds, and moves the GameObject there. Note that this takes more CPU time than __Discrete__. |
| __Sleeping Mode__ |Define how the GameObject "sleeps" to save processor time when it is at rest. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Never Sleep |Sleeping is disabled (this should be avoided where possible, as it can impact system resources). |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Start Awake |GameObject is initially awake. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Start Asleep |GameObject is initially asleep but can be woken by collisions. |
| __Interpolate__ |Define how the GameObject’s movement is interpolated between physics updates (useful when motion tends to be jerky). |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;None |No movement smoothing is applied. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Interpolate |Movement is smoothed based on the GameObject’s positions in previous frames. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Extrapolate |Movement is smoothed based on an estimate of its position in the next frame. |
| __Constraints__ |Define any restrictions on the Rigidbody 2D’s motion. |
| __Freeze Position__ |Stops the Rigidbody 2D moving in the world X & Y axes selectively. |
| __Freeze Rotation__ |Stops the Rigidbody 2D rotating around the Z axes selectively. |


### Body Type: Kinematic

![](../uploads/Main/Rigidbody2D_Kinematic.png)

A __Kinematic__ Rigidbody 2D is designed to move under simulation, but only under very explicit user control. While a __Dynamic__ Rigidbody 2D is affected by gravity and forces, a __Kinematic__ Rigidbody 2D isn’t. For this reason, it is fast and has a lower demand on system resources than a __Dynamic__ Rigidbody 2D. __Kinematic__ Rigidbody 2D is designed to be repositioned explicitly via [Rigidbody2D.MovePosition](http://docs.unity3d.com/ScriptReference/Rigidbody2D.MovePosition.html) or [Rigidbody2D.MoveRotation](http://docs.unity3d.com/ScriptReference/Rigidbody2D.MoveRotation.html). Use physics queries to detect collisions, and scripts to decide where and how the Rigidbody 2D should move. 

A __Kinematic__ Rigidbody 2D does still move via its velocity, but the velocity is not affected by forces or gravity. A __Kinematic__ Rigidbody 2D does not collide with other __Kinematic__ Rigidbody 2Ds or with __Static__ Rigidbody 2Ds; it only collides with __Dynamic__ Rigidbody 2Ds. Similar to a __Static__ Rigidbody 2D (see below), a __Kinematic__ Rigidbody 2D behaves like an immovable object (as if it has infinite mass) during collisions. Mass-related properties are not available with this Body Type.

|**Property:** |**Function:** |
|:---|:---|
| __Body Type__ |Set the RigidBody 2D’s component settings, so that you can manipulate movement (position and rotation) behavior and Collider 2D interaction. <br/>Options are: __Dynamic__, __Kinematic__, __Static__ |
| __Material__ |Use this to specify a common material for all Collider 2Ds attached to a specific parent Rigidbody 2D. <br/>**Note:** A Collider 2D uses its own Material property if it has one set. If there is no Material specified here or in the Collider 2D, the default option is __None (Physics Material 2D)__. This uses a default Material which you can set in the [Physics 2D Settings](class-Physics2DManager) window. <br/>A Collider 2D uses the following order of priority to determine which __Material__ setting to use: <br/>1. A Physics Material 2D specified on the Collider 2D itself.<br/> 2. A Physics Material 2D specified on the attached Rigidbody 2D.<br/> A Physics Material 2D default material specified in the [Physics 2D Settings](class-Physics2DManager).<br/> **TIP:** Use this to ensure that all Collider 2Ds attached to the same __Static__ Body Type Rigidbody 2D can all use the same Material. |
| __Simulated__ |Enable __Simulated__ (check the box) if you want the Rigidbody 2D and any attached Collider 2Ds and Joint 2Ds to interact with the physics simulation during run time. If this is disabled (the box is unchecked), these components do not interact with the simulation. See [Rigidbody 2D properties: Simulated](#SimulatedProperty), below, for more details. This box is checked by default. |
| __Use Full Kinematic Contacts__ |Enable this setting (check the box) if you want the __Kinematic__ Rigidbody 2D to collide with all Rigidbody 2D Body Types. This is similar to a __Dynamic__ Rigidbody 2D, except the __Kinematic__ Rigidbody 2D is not moved by the physics engine when contacting another Rigidbody 2D component; instead it acts as an immovable object, with infinite mass. When __Use Full Kinematic Contacts__ is disabled, the __Kinematic__ Rigidbody 2D only collides with __Dynamic__ Rigidbody 2Ds. See [Rigidbody 2D properties: Use Full Kinematic Contacts](#UseFullKinematicContactsProperty), below, for more details. This box is unchecked by default.|
| __Collision Detection__ |Define how collisions between Collider 2D are detected. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Discrete | When you set the __Collision Detection__ to __Discrete__, GameObjects with Rigidbody 2Ds and Collider 2Ds can overlap or pass through each other during a physics update, if they are moving fast enough. Collision contacts are only generated at the new position.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Continuous | When the __Collision Detection__ is set to __Continuous__, GameObjects with Rigidbody 2Ds and Collider 2Ds do not pass through each other during an update. Instead, Unity calculates the first impact point of any of the Collider 2Ds, and moves the GameObject there. Note that this takes more CPU time than __Discrete__. |
| __Sleeping Mode__ |Define how the GameObject "sleeps" to save processor time when it is at rest. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Never Sleep |Sleeping is disabled (this should be avoided where possible, as it can impact system resources). |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Start Awake |GameObject is initially awake. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Start Asleep |GameObject is initially asleep but can be woken by collisions. |
| __Interpolate__ |Define how the GameObject’s movement is interpolated between physics updates (useful when motion tends to be jerky). |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;None |No movement smoothing is applied. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Interpolate |Movement is smoothed based on the GameObject’s positions in previous frames. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Extrapolate |Movement is smoothed based on an estimate of its position in the next frame. |
| __Constraints__ |Define any restrictions on the Rigidbody 2D’s motion. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Freeze Position |Stops the Rigidbody 2D moving in the world's x & y axes selectively. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Freeze Rotation |Stops the Rigidbody 2D rotating around the world's z axis selectively. |


### Body Type: Static

![](../uploads/Main/Rigidbody2D_Static.png)

A __Static__ Rigidbody 2D is designed to not move under simulation at all; if anything collides with it, a __Static__ Rigidbody 2D behaves like an immovable object (as though it has infinite mass). It is also the least resource-intensive body type to use. A __Static__ body only collides with __Dynamic__ Rigidbody 2Ds. Having two __Static__ Rigidbody 2Ds collide is not supported, since they are not designed to move. 

Only a very limited set of properties are available for this Body Type.

|**Property:** |**Function:** |
|:---|:---|
| __Body Type__ |Set the RigidBody 2D’s component settings, so that you can manipulate movement (position and rotation) behavior and Collider 2D interaction. <br/>Options are: __Dynamic__, __Kinematic__, __Static__ |
| __Material__ |Use this to specify a common material for all Collider 2Ds attached to a specific parent Rigidbody 2D. <br/>**Note:** A Collider 2D uses its own Material property if it has one set. If there is no Material specified here or in the Collider 2D, the default option is __None (Physics Material 2D)__. This uses a default Material which you can set in the [Physics 2D Settings](class-Physics2DManager) window. <br/>A Collider 2D uses the following order of priority to determine which __Material__ setting to use: <br/>1. A Physics Material 2D specified on the Collider 2D itself.<br/> 2. A Physics Material 2D specified on the attached Rigidbody 2D.<br/> A Physics Material 2D default material specified in the [Physics 2D Settings](class-Physics2DManager).<br/> **TIP:** Use this to ensure that all Collider 2Ds attached to the same __Static__ Body Type Rigidbody 2D can all use the same Material. |
| __Simulated__ |Enable __Simulated__ (check the box) if you want the Rigidbody 2D and any attached Collider 2Ds and Joint 2Ds to interact with the physics simulation during run time. If this is disabled (the box is unchecked), these components do not interact with the simulation. See [Rigidbody 2D properties: Simulated](#SimulatedProperty), below, for more details. This box is checked by default. |

There are two ways to mark a Rigidbody 2D as __Static__: 

1. For the GameObject with the Collider 2D component not to have a Rigidbody 2D component at all. All such Collider 2Ds are internally considered to be attached to a single hidden __Static__ Rigidbody 2D component.

2. For the GameObject to have a Rigidbody 2D and for that Rigidbody 2D to be set to __Static__. 

Method 1 is a shorthand for making __Static__ Collider 2Ds. When creating large numbers of __Static__ Collider 2Ds, it is easier not to have to add a Rigidbody 2D for each GameObject with a Collider 2D. 

Method 2 exists for performance reasons. If a __Static__ Collider 2D needs to be moved or reconfigured at run time, it is faster to do so when it has its own Rigidbody 2D. If a group of Collider 2Ds needs to be moved or reconfigured at run time, it is faster to have them all be children of one parent Rigidbody 2D marked as __Static__ than to move each GameObject individually.

**Note:** As stated above, __Static__ Rigidbody 2Ds are designed not to move, and collisions between two __Static__ Rigidbody 2D objects that intersect are not registered. However, __Static__ Rigidbody 2Ds and __Kinematic__ Rigidbody 2Ds will interact with each other if one of their Collider 2Ds is set to be a trigger. There is also a feature that changes what a __Kinematic__ body will interact with (see [Use Full Kinematic Contacts](#UseFullKinematicContactsProperty), below).

## Rigidbody 2D properties

<a name="SimulatedProperty"></a>
### Simulated

Use the __Simulated__ property to stop (unchecked) and start (checked) a Rigidbody 2D and any attached Collider 2Ds and Joint 2Ds from interacting with the 2D physics simulation.  Changing this property is much more memory and processor-efficient than enabling or disabling individual Collider 2D and Joint 2D components.

When the __Simulation__ box is checked, the following occurs:

* The Rigidbody 2D moves via the simulation (gravity and physics forces are applied)
* Any attached Collider 2Ds continue creating new contacts and continuously re-evaluate contacts 
* Any attached Joint 2Ds are simulated and constrain the attached Rigidbody 2D
* All internal physics objects for Rigidbody 2D, Collider 2D & Joint 2D stay in memory

When the __Simulated__ box is unchecked, the following occurs:

* The Rigidbody 2D is not moved by the simulation (gravity and physics forces are not applied)
* The Rigidbody 2D does not create new contacts, and any attached Collider 2D contacts are destroyed
* Any attached Joint 2Ds are not simulated, and do not constrain any attached Rigidbody 2Ds
* All internal physics objects for Rigidbody 2D, Collider 2D and Joint 2D are left in memory

####Why is unchecking Simulated more efficient than individual component controls?

In the 2D physics simulation, a Rigidbody 2D component controls the position and rotation of attached Collider 2D components, and allows Joint 2D components to use these positions and rotations as anchor points. A Collider 2D moves when the Rigidbody 2D it is attached to moves. The Collider 2D then calculates contacts with other Collider 2Ds attached to other Rigidbody 2Ds. Joint 2Ds also constrain Rigidbody 2D positions and rotations. All of this takes simulation time.

You can stop and start individual elements of the 2D physics simulation by enabling and disabling components individually. You can do this on both Collider 2D and Joint 2D components. However, enabling and disabling individual elements of the physics simulations has memory use and processor power costs. When elements of the simulation are disabled, the 2D physics engine doesn't produce any internal physics-based objects to simulate. When elements of the simulation are enabled, the 2D physics engine does have internal physics-based objects to simulate. Enabling and disabling of 2D physics simulation components means internal GameObjects and physics-based components have to be created and destroyed; disabling the simulation is easier and more efficient than disabling individual components.

NOTE: When a Rigidbody 2D’s __Simulated__ option is unchecked, any attached Collider 2D is effectively ‘invisible’, that is; it cannot be detected by any physics queries, such as [Physics.Raycast](scriptref:Physics.Raycast.html).

<a name="UseFullKinematicContactsProperty"></a>
### Use Full Kinematic Contacts

Enable this setting (check the checkbox) if you want the __Kinematic__ Rigidbody 2D to collide with all Rigidbody 2D Body Types. This is similar to a __Dynamic__ Rigidbody 2D, except the __Kinematic__ Rigidbody 2D is not moved by the physics engine when contacting another Rigidbody 2D; it acts as an immovable object, with infinite mass.

When this setting is disabled (unchecked), a __Kinematic__ Rigidbody 2D only collides with __Dynamic__ Rigidbody 2Ds; it does not collide with other __Kinematic__ Rigidbody 2Ds or __Static__ Rigidbody 2Ds (note that trigger colliders are an exception to this rule).  This means that no collision scripting callbacks ([OnCollisionEnter](scriptRef:Collider2D.OnCollisionEnter2D.html), [OnCollisionStay](scriptRef:Collider2D.OnCollisionStay2D.html), [OnCollisionExit](scriptRef:Collider2D.OnCollisionExit2D.html)) occur. 

This  can be inconvenient when you are using physics queries (such as [Physics.Raycast](scriptref:Physics.Raycast.html)) to detect where and how a Rigidbody 2D should move, and when you require multiple __Kinematic__ Rigidbody 2Ds to interact with each other. Enable __Use Full Kinematic Contacts__ to make __Kinematic__ Rigidbody 2D components interact in this way.

__Use Full Kinematic Contacts__ allows explicit position and rotation control of a __Kinematic__ Rigidbody 2D, but still allows full collision callbacks. In a set-up where you need explicit control of all Rigidbody 2Ds, use __Kinematic__ Rigidbody 2Ds in place of __Dynamic__ Rigidbody 2Ds to still have full collision callback support.

