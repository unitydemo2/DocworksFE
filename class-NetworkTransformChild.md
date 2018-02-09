NetworkTransformChild
====================

The NetworkTransformChild component synchronizes the position and rotation of a child object of an object with a NetworkTransform component. The NetworkTransformChild component should be placed on the same root object as the NetworkTransform, and then the target slot populated with a child object from the heirarchy.

This class does not use physics, it simply synchronizes the position and rotation of the child and  lerps towards updated values to at a customizable rate.


Properties
----------

|**_Property:_** ||**_Function:_** |
|:---|:---|:---|
|__sendInterval__ ||How often in seconds the object sends updates. |
|__target__ || child transform to be synchronized. |
|__childIndex__ || A unique Identifier for this NetworkTransformChild component on this root object (read only). |
|__syncRotationAxis__ ||Which axis to use for rotation. |
|__rotationSyncCompression__ ||What kind of compression to use for rotation. |
|__movementTheshold__ ||The threshold to not send position updates. |
|__snapThreshold__ ||The threshold to "pop" instead of interpolate. |
|__interpolateRotation__ ||Factor to control rotation interpolation. |
|__interpolateMovement__ ||Factor to control movement interpolation. |




