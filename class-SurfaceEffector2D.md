Surface Effector 2D
=========

The Surface Effector 2D applies tangent forces along the surfaces of colliders used by the effector in an attempt to match a specified speed along the surface.  This is analogous to a conveyor belt.

Colliders that you use with the effector would typically be set as non-triggers so that other colliders can come into contact with the surface.


![The Surface Effector 2D Inspector](../uploads/Main/SurfaceEffector2DInspector.png) 

Properties
----------


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Use Collider Mask__ |Should the 'Collider Mask' property be used?  If not then the global collision matrix will be used as is the default for all colliders.|
|__Collider Mask__ |The mask used to select specific layers allowed to interact with the effector. |
|__Speed__ |The speed to be maintained along the surface. |
|__Speed Variation__ |A random increase in the speed (anywhere between 0 and the Speed Variation value) will be applied to the speed. If a negative number is entered here, a random _reduction_ in the speed will be applied.|
|__Force Scale__ |Allows scaling of the force that is applied when the effector attempts to attain the specified speed along the surface.  If 0 then no force is applied is is effectively disabled.  If 1 then the full force is applied.  It can be thought of as how fast the target object is modified to meet the specified speed with lower values being slower and higher values being quicker.  Care should be taken however as applying the full force will easily counteract any other forces being applied to the target object such as jump or other movement forces.  For this reason, a value less than 1 is advised. |
|__Use Contact Force__ |Should the force be applied at the point of contact between the surface and the target collider?  Using contact forces can cause the target object to rotate whereas not using contact forces won't. |
|__Use Friction__ |Should friction be used when contacting the surface? |
|__Use Bounce__ |Should bounce be used when contacting the surface? |
