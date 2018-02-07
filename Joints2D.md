# 2D Joints

As the name implies, joints attach GameObjects together. You can only attach 2D joints to GameObjects which have a Rigidbody 2D component attached, or to a fixed position in world space.

2D joints all have names ending ‘2D'. A joint named without a ‘2D’ ending is a 3D joint. 2D joints work with game objects in 2D and 3D joints work with game objects in 3D.

(See **Details and Hints**, below, for useful background information on all 2D joints.)

There are different types of 2D joints. See each joint reference page for detailed information about their properties:

* [Distance Joint 2D](class-DistanceJoint2D)  - attaches two game objects controlled by rigidbody physics together and keeps them a certain distance apart.

* [Fixed Joint 2D](class-FixedJoint2D) - keeps two objects in a position relative to each other, so the objects are always offset at a given position and angle. For example,  objects that need to react as if they are rigidly connected: They can't move away from each other, they can't move closer together, and they can't rotate with respect to each other. You can also use this joint to create a less rigid connection that flexes.

* [Friction Joint 2D](class-FrictionJoint2D) -  reduces both the linear and angular velocities between two game objects controlled by rigidbody physics to zero (ie: it slows them down and stops them).  For example; a platform that rotates but resists that movement. 

* [Hinge Joint 2D](class-HingeJoint2D)- allows a game object controlled by rigidbody physics to be attached to a point in space around which it can rotate. For example; the pivot on a pair of scissors.

* [Relative Joint 2D](class-RelativeJoint2D) - allows two game objects controlled by rigidbody physics to maintain a position based on each other's location. Use this joint to keep two objects offset from each other. For example;  a space-shooter game where the player has extra gun batteries that follow them.

* [Slider Joint 2D](class-SliderJoint2D) - allows a game object controlled by rigidbody physics to slide along a line in space, like sliding doors, for example.

* [Spring Joint 2D](class-SpringJoint2D) - allows two game objects controlled by rigidbody physics to be attached together as if by a spring.

* [Target Joint 2D](class-TargetJoint2D) - connects to a specified target, rather than another rigid body object, as other joints do. It is a spring type joint, which you could use for picking up and moving an object acting under gravity, for example.

* [Wheel Joint 2D](class-WheelJoint2D) - simulates wheels and suspension.

##Details and Hints

### Constraints

All joints provide one or more constraints that apply to Rigidbody 2D behaviour.  A constraint is a ‘rule’ which the joint will try to ensure isn’t permanently broken.  There are different types of constraints available but usually a joint will only provide a few of them, sometimes only one.  Some constraints limit behaviour such as ensuring a rigid body stays on a line, or in a certain position.  Some are ‘driving’ constraints such as a motor that rotates or moves a  rigid body object, trying to maintain a certain speed.

### Temporarily breaking constraints

The physics system expects that constraints do become temporarily broken; the objects may move further apart than their distance constraint tells them, or objects may move faster than their motor-speed constraint.  When a constraint isn’t broken, the joint doesn’t apply any forces and does little work.  It is when a constraint is broken that the joint applies forces to fix the constraint: So for the 'driving' constraints mentioned above, it maintains a distance or ensures a motor-speed.  This force, however, doesn’t always instantaneously fix the constraint. Although it usually happens very fast, it can happen over time.  

This time lag can lead to joints ‘stretching’ or seeming ‘soft’. The lag happens because the physics system is trying to apply joint-forces to fix constraints,  whilst at the same time other game physics forces are acting to break constraints.  In addition to the conflicting forces acting on game objects, some joints are more stable and react faster than others. 

Whatever constraints the joint provides, the joint only uses forces to fix the constraint.  These are either a linear (straight line) force or angular (torque) force. 

**HINT:** Given the conflicing forces acting on joints,  it is always good to be cautious when applying large forces to rigid body objects that have joints attached, especially those with large masses. 

## Permanently breaking joints

All joints have the ability to stop working completely (that is break) when a force exceeds a specified limit. The limit that causes breaking due to excessive linear force is called the "break force".  The limit that causes breaking due to excessive torque force is called the "break torque".
 
 * If a joint applies linear force, then it has a __Break Force__ option.
 * If a joint applies an angular (rotation) force then it has a __Break Torque__ option.  
 

Both these limits are pre-set to __Infinity__: This means that they have no limit.  

When a __Break Force__ or __Break Torque__ limit is exceeded, the joint breaks and the component deletes itself from its GameObject.
