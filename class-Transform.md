#Transform

The __Transform__ component determines the __Position__, __Rotation__, and __Scale__ of each object in the scene. Every GameObject has a Transform.


![](../uploads/Main/TransformExample1.png) 


##Properties


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Position__ |Position of the Transform in X, Y, and Z coordinates. |
|__Rotation__ |Rotation of the Transform around the X, Y, and Z axes, measured in degrees. |
|__Scale__ |Scale of the Transform along X, Y, and Z axes. Value "1" is the original size (size at which the object was imported). |

The position, rotation and scale values of a Transform are measured relative to the Transform's parent. If the Transform has no parent, the properties are measured in world space.
