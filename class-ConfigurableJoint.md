#Configurable Joint


__Configurable Joints__ are extremely customisable since they incorporate all the functionality of the other joint types. You can use them to create anything from adapted versions of the existing joints to highly specialised joints of your own design.

##Properties

![](../uploads/Main/ConfigurableJointProps.png) 

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Connected Body__ |The other Rigidbody object to which the joint is connected. You can set this to _None_ to indicate that the joint is attached to a fixed position in space rather than another Rigidbody. |
|__Anchor__ |The point where the center of the joint is defined. All physics-based simulation will use this point as the center in calculations |
|__Axis__ |The local axis that will define the object's natural rotation based on physics simulation |
|__Auto Configure Connected Anchor__ |If this is enabled, then the Connected Anchor position will be calculated automatically to match the global position of the anchor property. This is the default behavior. If this is disabled, you can configure the position of the connected anchor manually.|
|__Connected Anchor__ |Manual configuration of the connected anchor position. |
|__Secondary Axis__ |Together, __Axis__ and __Secondary Axis__ define the local coordinate system of the joint. The third axis is set to be orthogonal to the other two. |
|__X, Y, Z Motion__ |Allow movement along the X, Y or Z axes to be _Free_, completely _Locked_, or _Limited_ according to the limit properties described below. |
|__Angular X, Y, Z Motion__ |Allow rotation around the X, Y or Z axes to be _Free_, completely _Locked_, or _Limited_ according to the limit properties described below.  |
|__Linear Limit Spring__ |A spring force applied to pull the object back when it goes past the limit position. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Spring__ |The spring force. If this value is set to zero then the limit will be impassable; a value other than zero will make the limit elastic. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Damper__ |The reduction of the spring force in proportion to the speed of the joint's movement. Setting a value above zero allows the joint to "dampen" oscillations which would otherwise carry on indefinitely. |
|__Linear Limit__ |Limit on the joint's linear movement (ie, movement over distance rather than rotation), specified as a distance from the joint's origin. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Limit__ |The distance in world units from the origin to the limit. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Bounciness__ |Bounce force applied to the object to push it back when it reaches the limit distance. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Contact Distance__ |The minimum distance tolerance (between the joint position and the limit) at which the limit will be enforced. A high tolerance makes the limit less likely to be violated when the object is moving fast. However, this will also require the limit to be taken into account by the physics simulation more often and this will tend to reduce performance slightly. |
|__Angular X Limit Spring__ |A spring torque applied to rotate the object back when it goes past the limit angle of the joint. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Spring__ |The spring torque. If this value is set to zero then the limit will be impassable; a value other than zero will make the limit elastic. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Damper__ |The reduction of the spring torque in proportion to the speed of the joint's rotation. Setting a value above zero allows the joint to "dampen" oscillations which would otherwise carry on indefinitely. |
|__Low Angular X Limit__ |Lower limit on the joint's rotation around the X axis, specified as a angle from the joint's original rotation. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Limit__ |The limit angle. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Bounciness__ |Bounce torque applied to the object when its rotation reaches the limit angle. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Contact Distance__ |The minimum angular tolerance (between the joint angle and the limit) at which the limit will be enforced. A high tolerance makes the limit less likely to be violated when the object is moving fast. However, this will also require the limit to be taken into account by the physics simulation more often and this will tend to reduce performance slightly. |
|__High Angular XLimit__ |This is similar to the _Low Angular X Limit_ property described above but it determines the upper angular limit of the joint's rotation rather than the lower limit. |
|__Angular YZ Limit Spring__ |This is similar to the _Angular X Limit Spring_ described above but applies to rotation around both the Y and Z axes. |
|__Angular Y Limit__ |Analogous to the _Angular X Limit_ properties described above but applies to the Y axis and regards both the upper and lower angular limits as being the same. |
|__Angular Z Limit__ |Analogous to the _Angular X Limit_ properties described above but applies to the Z axis and regards both the upper and lower angular limits as being the same. |
|__Target Position__ |The target position that the joint's drive force should move it to. |
|__Target Velocity__ |The desired velocity with which the joint should move to the _Target Position_ under the drive force. |
|__XDrive__ |The drive force that moves the joint linearly along its local X axis. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Mode__ |The mode determines whether the joint should move to reach a specified __Position__, a specified __Velocity__ or both. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Position Spring__ |The spring force that moves the joint towards its target position. This is only used when the drive mode is set to _Position_ or _Position and Velocity_. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Position Damper__ |The reduction of the spring force in proportion to the speed of the joint's movement. Setting a value above zero allows the joint to "dampen" oscillations which would otherwise carry on indefinitely. This is only used when the drive mode is set to _Position_ or _Position and Velocity_. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Maximum Force__ |The force used to accelerate the joint toward its target velocity. This is only used when the drive mode is set to _Velocity_ or _Position and Velocity_. |
|__YDrive__ |This is analogous to the _X Drive_ described above but applies to the joint's Y axis. |
|__ZDrive__ |This is analogous to the _X Drive_ described above but applies to the joint's Z axis. |
|__Target Rotation__ |The orientation that the joint's rotational drive should rotate towards, specified as a [quaternion](ScriptRef:Quaternion.html). |
|__Target Angular Velocity__ |The angular velocity that the joint's rotational drive should aim to achieve. This is specified as a vector whose length specifies the rotational speed and whose direction defines the axis of rotation. |
|__Rotation Drive Mode__ |The way in which the drive force will be applied to the object to rotate it to the target orientation. If the mode is set to _X and YZ_, the torque will be applied around these axes as specified by the _Angular X/YZ Drive_ properties described below. If __Slerp__ mode is used then the _Slerp Drive_ properties will determine the drive torque. |
|__Angular X Drive__ |This specifies how the joint will be rotated by the drive torque around its local X axis. It is used only if the _Rotation Drive Mode_ property described above is set to _X &amp; YZ_. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Mode__ |The mode determines whether the joint should move to reach a specified angular __Position__, a specified angular __Velocity__ or both. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Position Spring__ |The spring torque that rotates the joint towards its target position. This is only used when the drive mode is set to _Position_ or _Position and Velocity_. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Position Damper__ |The reduction of the spring torque in proportion to the speed of the joint's movement. Setting a value above zero allows the joint to "dampen" oscillations which would otherwise carry on indefinitely. This is only used when the drive mode is set to _Position_ or _Position and Velocity_. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Maximum Force__ |The torque used to accelerate the joint toward its target velocity. This is only used when the drive mode is set to _Velocity_ or _Position and Velocity_. |
|__Angular YZDrive__ |This is analogous to the _Angular X Drive_ described above but applies to both the joint's Y and Z axes. |
|__Slerp Drive__ |This specifies how the joint will be rotated by the drive torque around all local axes. It is used only if the _Rotation Drive Mode_ property described above is set to _Slerp_. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Mode__ |The mode determines whether the joint should move to reach a specified angular __Position__, a specified angular __Velocity__ or both. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Position Spring__ |The spring torque that rotates the joint towards its target position. This is only used when the drive mode is set to _Position_ or _Position and Velocity_. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Position Damper__ |The reduction of the spring torque in proportion to the speed of the joint's movement. Setting a value above zero allows the joint to "dampen" oscillations which would otherwise carry on indefinitely. This is only used when the drive mode is set to _Position_ or _Position and Velocity_. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Maximum Force__ |The torque used to accelerate the joint toward its target velocity. This is only used when the drive mode is set to _Velocity_ or _Position and Velocity_. |
|__Projection Mode__ |This defines how the joint will be snapped back to its constraints when it unexpectedly moves beyond them (due to the physics engine being unable to reconcile the current combination of forces within the simulation). The options are _None_ and _Position and Rotation_. |
|__Projection Distance__ |The distance the joint must move beyond its constraints before the physics engine will attempt to snap it back to an acceptable position. |
|__Projection Angle__ |The angle the joint must rotate beyond its constraints before the physics engine will attempt to snap it back to an acceptable position. |
|__Configured in World Space__ |Should the values set by the various target and drive properties be calculated in world space instead of the object's local space? |
|__Swap Bodies__ |If enabled, this will make the joint behave as though the component were attached to the connected Rigidbody (ie, the other end of the joint). |
|__Break Force__ |If the joint is pushed beyond its constraints by a force larger than this value then the joint will be permanently "broken" and deleted. |
|__Break Torque__ |If the joint is rotated beyond its constraints by a torque larger than this value then the joint will be permanently "broken" and deleted.  |
|__Enable Collision__ |Should the object with the joint be able to collide with the connected object (as opposed to just passing through each other)? |
|__Enable Preprocessing__ |If preprocessing is disabled then certain "impossible" configurations of the joint will be kept more stable rather than drifting wildly out of control. |


##Details

Like the other joints, the Configurable Joint allows you to restrict the movement of an object but also to drive it to a target velocity or position using forces. However, there are many configuration options available and they can be quite subtle when used in combination; you may need to experiment with different options to get the joint to behave exactly the way you want.


###Constraining Movement

You can constrain both translational movement and rotation on each axis independently using the _X, Y, Z Motion_ and _X, Y, Z Rotation_ properties. If _Configured In World Space_ is enabled then movements will be constrained to the world axes rather than the object's local axes. Each of these properties can be set to _Locked_, _Limited_ or _Free_:

* A **Locked** axis will allow no movement at all. For example, an object locked in the world Y axis cannot move up or down.
* A **Limited** axis allows free movement between predefined limits, as explained below. For example, a gun turret might be given a restricted arc of fire by limiting its Y rotation to a specific angular range.
* A **Free** axis allows any movement.

You can limit translational movement using the _Linear Limit_ property, which defines the maximum distance the joint can move from its point of origin. (measured along each axis separately). For example, you could constrain the puck for an air hockey table by locking the joint in the Y axis (in world space), leaving it free in the Z axis and setting the limit for the X axis to fit the width of the table; the puck would then be constrained to stay within the playing area.

![](../uploads/Main/XZLimit.svg)

You can also limit rotation using the _Angular Limit_ properties. Unlike the linear limit, these allow you to specify different limit values for each axis. Additionally, you can also define separate upper and lower limits on the angle of rotation for the X axis (the other two axes use the same angle either side of the original rotation). For example, you could construct a "teeter table" using a flat plane with a joint constrained to allow slight tilting in the X and Z directions while leaving the Y rotation locked.

####Bounciness and Springs

By default, a joint simply stops moving when it runs into its limit. However, an inelastic collision like this is rare in the real world and so it is useful to add some feeling of bounce to a constrained joint. You can use the _Bounciness_ property of the linear and angular limits to make the constrained object bounce back after it hits its limit. Most collisions will look more natural with a small amount of bounciness but you can also set this property higher to simulate unusually bouncy boundaries like, say, the cushions of a pool table.

![Bouncy joint does not cross the limit](../uploads/Main/CJointBounciness.svg)

The joint limits can be softened further using the spring properties: _Linear Limit Spring_ for translation and _Angular X/YZ Limit Spring_ for rotation. If you set the _Spring_ property to a value above zero, the joint will not abruptly stop moving when it hits a limit but will be drawn back to the limit position by a spring force (the strength of the force is determined by the _Spring_ value). By default, the spring is perfectly elastic and will tend to catapult the joint back in the direction opposite to the collision. However, you can use the _Damper_ property to reduce the elasticity and return the joint to the limit more gently. For example, you might use a spring joint to create a lever that can be pulled to the left or right but then springs back to an upright position. If the springs are perfectly elastic then the lever will tend to oscillate back and forth around the centre point after it is released. However, if you add enough damping then the spring will rapidly settle down to the neutral position.

![Spring joint crosses the limit but is pulled back to it](../uploads/Main/CJointSpring.svg)

###Drive forces

Not only can a joint react to the movements of the attached object, but it can also actively apply _drive forces_ to set the object in motion. Some joints simple need to keep the object moving at a constant speed as with, say, a rotary motor turning a fan blade. You can set your desired velocity for such joints using the _Target Velocity_ and _Target Angluar Velocity_ properties. You might also require joints that move their object towards a particular position in space (or a particular orientation); you can set these using the _Target Position_ and _Target Rotation_ properties. For example, you could implement a forklift by mounting the forks on a configurable joint and then setting the target height to raise them from a script.

With the target set, the _X, Y, Z Drive_ and _Angular X/YZ Drive_ (or alternatively _Slerp Drive_) properties then specify the force used to push the joint toward it. The Drives' _Mode_ property selects whether the joint should seek a target position, velocity or both. The _Position Spring_ and _Position Damper_ work in the same way as for the joint limits when seeking a target position. In velocity mode, the spring force is dependent on the "distance" between the current velocity and the target velocity; the damper helps the velocity to settle at the chosen value rather than oscillating endlessly around it. The _Maximum Force_ property is a final refinement that prevents the force applied by the spring from exceeding a limit value regardless of how far the joint is from its target. This prevents the circumstance where a joint stretched far from its target rapidly snaps the object back in an uncontrolled way.

Note that with all the drive forces (except for _Slerp Drive_, described below), the force is applied separately in each axis. So, for example, you could implement a spacecraft that has a high forward flying speed but a relatively low speed in sideways steering motion.


####Slerp Drive

While the other drive modes apply forces in separate axes, _Slerp Drive_ uses the Quaternion's spherical interpolation or "slerp" functionality to reorient the joint. Rather than isolating individual axes, the slerp process essentially finds the minimum total rotation that will take the object from the current orientation to the target and applies it on all axes as necessary. Slerp drive is slightly easier to configure and fine for most purposes but does not allow you to specify different drive forces for the X and Y/Z axes.

To enable Slerp drive, you should change the _Rotation Drive Mode_ property from _X and YZ_ to _Slerp_. Note that the modes are mutually exclusive; the joint will use either the _Angular X/YZ Drive_ values or the _Slerp Drive_ values but not both together.
