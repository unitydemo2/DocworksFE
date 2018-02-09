Constant Force
==============


__Constant Force__ is a quick utility for adding constant forces to a __Rigidbody__. This works great for one shot objects like rockets, if you don't want it to start with a large velocity but instead accelerate.


![](../uploads/Main/Inspector-ConstantForce.png) 


Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Force__ |The vector of a force to be applied in world space. |
|__Relative Force__ |The vector of a force to be applied in the object's local space. |
|__Torque__ |The vector of a torque, applied in world space. The object will begin spinning _around_ this vector. The longer the vector is, the faster the rotation. |
|__Relative Torque__ |The vector of a torque, applied in local space. The object will begin spinning _around_ this vector. The longer the vector is, the faster the rotation. |


###Details

To make a rocket that accelerates forward set the __Relative Force__ to be along the positive z-axis. Then use the Rigidbody's __Drag__ property to make it not exceed some maximum velocity (the higher the drag the lower the maximum velocity will be). In the Rigidbody, also make sure to turn off gravity so that the rocket will always stay on its path.

Hints
-----


* To make an object flow upwards, add a Constant Force with the __Force__ property having a positive Y value.
* To make an object fly forwards, add a Constant Force with the __Relative Force__ property having a positive Z value.
