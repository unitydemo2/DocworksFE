Constant Force 2D
=========

__Constant Force 2D__ is a quick utility for adding constant forces to a __Rigidbody 2D__. This works well for one-shot objects like rockets, if you want them to accelerate over time rather than starting with a large velocity.

Constant Force 2D applies both linear and torque (angular) forces continuously to the Rigidbody 2D, each time the physics engine updates at runtime.

![The Constant Force 2D Inspector](../uploads/Main/ConstantForce2DInspector.png) 

Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Force__ |The linear force applied to the Rigidbody 2D at each physics update. |
|__Relative Force__ |The linear force, relative to the Rigidbody 2D coordinate system, applied each physics update. |
|__Torque__ |The torque applied to the Rigidbody 2D at each physics update. |
