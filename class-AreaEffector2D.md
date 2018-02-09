Area Effector 2D
=========

The Area Effector 2D applies forces within an area defined by the attached Collider 2Ds when another (target) Collider 2D comes into contact with the Effector 2D. You can configure the force at any angle with a specific magnitude and random variation on that magnitude. You can also apply both linear and angular drag forces to slow down Rigidbody 2Ds.

Collider 2Ds that you use with the Area Effector 2D would typically be set as triggers, so that other Collider 2Ds can overlap with it to have forces applied. Non-triggers will still work, but forces will only be applied when Collider 2Ds come into contact with them.


![The Area Effector 2D Inspector](../uploads/Main/AreaEffector2DInspector.png) 

Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Use Collider Mask__ |Check to enable use of the __Collider Mask__ property? If this is not enabled, the Global Collision Matrix will be used as the default for all Collider 2Ds.|
|__Collider Mask__ |The mask used to select specific Layers allowed to interact with the Area Effector 2D. |
|__Use Global Angle__ |Check this to define the __Force Angle__ as a global (world-space) angle. If this is not checked, the __Force Angle__ is considered a local angle by the physics engine. |
|__Force Angle__ |The angle of the force to be applied. |
|__Force Magnitude__ |The magnitude of the force to be applied. |
|__Force Variation__ |The variation of the magnitude of the force to be applied. |
|__Drag__ |The linear drag to apply to Rigidbody 2Ds. |
|__Angular Drag__ |The angular drag to apply to Rigidbody 2Ds. |
|__Force Target__ |The point on a target GameObject where the Area Effector 2D applies any force.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Collider|The target point is defined as the current position of the Collider 2D. Applying force here can generate torque (rotation) if the Collider 2D isn't positioned at the center of mass.|
|&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;Rigidbody|The target point is defined as the current center-of-mass of the Rigidbody 2D. Applying force here will never generate torque (rotation). |

