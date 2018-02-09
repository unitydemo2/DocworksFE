Platform Effector 2D
=========

The Platform Effector 2D applies various "platform" behaviour such as one-way collisions, removal of side-friction/bounce etc.  

Colliders that you use with the effector would typically not be set as triggers so that other colliders can collide with it.

![The Platform Effector 2D Inspector](../uploads/Main/PlatformEffector2DInspector.png) 

Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Use Collider Mask__ |Should the 'Collider Mask' property be used?  If not then the global collision matrix will be used as is the default for all colliders.|
|__Collider Mask__ |	The mask used to select specific layers allowed to interact with the effector. |
|__Use One Way__ |Should one-way collision behaviour be used? |
|__Use One Way Grouping__ |Ensures that all contacts disabled by the one-way behaviour act on all colliders. This is useful when multiple colliders are used on the object passing through the platform and they all need to act together as a group.|
|__Surface Arc__ |The angle of an arc centered on the local 'up' the defines the surface which doesn't allow colliders to pass.  Anything outside of this arc is considered for one-way collision.|
|__Use Side Friction__ |Should friction should be used on the platform sides? |
|__Use Side Bounce__ |Should bounce should be used on the platform sides? |
|__Side Arc__ |The angle of an arc that defines the sides of the platform centered on the local 'left' and 'right' of the effector. Any collision normals within this arc are considered for the 'side' behaviours. |
