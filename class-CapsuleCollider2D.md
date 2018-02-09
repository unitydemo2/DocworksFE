# Capsule Collider 2D

The Capsule Collider 2D component is a 2D physics primitive that you can elongate in either a vertical or horizontal direction. The capsule shape has no vertex corners; it has a continuous circumference, which doesn’t get easily caught on other collider corners. The capsule shape is solid, so any other Collider 2Ds that are fully inside the capsule are considered to be in contact with the capsule and are forced out of it over time.


![](../uploads/Main/CapsuleCollider2D.png)


|**Property:** |**Function:** |
|:---|:---|
| __Material__ |Use this to define the physics material used by the Capsule Collider 2D. This overrides any Rigidbody 2D or global physics collider. |
| __Is Trigger__ |Check this box to specify that the Capsule Collider 2D triggers events. If you check this box, the physics engine ignores this collider. |
| __Used by Effector__ |Check this box to specify that an attached Effector uses this Capsule Collider 2D. |
| __Offset__ |Use this to set the local offset of the Capsule Collider 2D geometry. |
| __Size__ |Use this to define a box size. This box defines the region that the Capsule Collider 2D fills. |
| __Direction__ |Set this to either Vertical or Horizontal. This controls which way round the capsule sets: specifically, it defines the positioning of the semi-circular end-caps. |

The settings that define the Capsule Collider 2D are __Size__ and __Direction__. Both the Size and Direction properties refer to __X__ and __Y__ (horizontal and vertical, respectively) in the local space of the Capsule Collider 2D, and not in world-space.


A typical way to set up the Capsule Collider 2D is to set the __Size__ to match the __Direction__. For example, if the Capsule Collider 2D’s __Direction__ is __Vertical__, the __Size__ of __X__ is 0.5 and the __Size__ of __Y__ is 1, this makes the vertical direction capsule taller, rather than wider.

In the example below, the __X__ and __Y__ are represented by the yellow lines.

![An example of a Capsule Collider 2D set so the __Size__ matches __Direction__](../uploads/Main/CapsuleCollider2D-Example1.png)

##Capsule configuration examples

You can change the Capsule Collider 2D with different configurations. Below are some examples.

Note that when the __X __and __Y__ of the __Size__ property are the same, the Capsule Collider 2D always approximates to a circle.

![Examples of Capsule Collider 2D configurations](../uploads/Main/CapsuleCollider2D-Example2.png)

###Tip

A known issue in physics engines (including Box 2D) is that moving across multiple colliders, even colliders that are perfectly aligned numerically, causes one or both of the colliders to register a collision between the two colliders. This can cause the collider to slow down or stop. 

While the Capsule Collider 2D can help reduce this problem, it isn’t a solution to it. A better solution is to use a single collider for a surface; for example, the Edge Collider 2D. 

