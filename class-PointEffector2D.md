Point Effector 2D
=========

The Point Effector 2D applies forces to attract/repulse against a source point which can be defined as the position of the rigid-body or the center of a collider used by the effector.  When another (target) collider comes into contact with the effector then a force is applied to the target.  Where the force is applied and how it is calculated can be controlled.

Colliders that you use with the effector would typically be set as triggers so that other colliders can overlap with it to have forces applied however, non-triggers will still work but forces will only be applied when colliders come into contact with it.


![The Point Effector 2D Inspector](../uploads/Main/PointEffector2DInspector.png) 

Properties
----------

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Use Collider Mask__ |Should the 'Collider Mask' property be used?  If not then the global collision matrix will be used as is the default for all colliders.|
|__Collider Mask__ |The mask used to select specific layers allowed to interact with the effector. |
|__Force  Magnitude__ |The magnitude of the force to be applied. |
|__Force Variation__ |The variation of the magnitude of the force to be applied. |
|__Distance Scale__ |The scale applied to the distance between the source and target.  When calculating the distance, it is scaled by this amount allowing the effective distance to be changed which controls the magnitude of the force applied. |
|__Drag__ |The linear drag to apply to rigid-bodies. |
|__Angular Drag__ |The angular drag to apply to rigid-bodies. |
|__Force Source__ |The force source is the point that attracts or repels target objects.  The distance from the target is defined from this point. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Collider__|The source point is defined as the current position of the collider.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Rigidbody__|The source point is defined as the current position of the rigidbody.|
|__Force Target__ |The force target is the point on a target object where the effector applies any force.  The distance to the source is defined from this point. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Collider__|The target point is defined as the current position of the collider.  Applying force here can generate torque (cause the target to rotate) if the collider isn't positioned at the center-of-mass.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Rigidbody__|The target point is defined as the current center-of-mass of the rigidbody.  Applying force here will never generate torque (cause the target to rotate). |
|__Force Mode__ |How the force is calculated. |
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Constant__|The force is applied ignoring how far apart the source and target are.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Inverse Linear__|The force is applied as a function of the inverse-linear distance between the source and target.  When the source and target are in the same position then the full force is applied but it falls-off linearly as they move apart.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;__Inverse Squared__|The force is applied as a function of the inverse-squred distance between the source and target.  When the source and target are in the same position then the full force is applied but it falls-off squared as they move apart.  This is similar to real-world gravity.|