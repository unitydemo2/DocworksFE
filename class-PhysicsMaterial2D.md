Physics Material 2D
===================


A __Physics Material 2D__ is used to adjust the friction and bounce that occurs between 2D physics objects when they collide. You can create a Physics Material 2D from the Assets menu (__Assets &gt; Create &gt; Physics2D Material__ ).


![](../uploads/Main/PhysicsMaterial2DInspector.png) 


Properties
----------



|**_Property:_** |**_Function:_** |
|:---|:---|
|__Friction__ |Coefficient of friction for this collider. |
|__Bounciness__ |The degree to which collisions rebound from the surface. A value of 0 indicates no bounce while a value of 1 indicates a perfect bounce with no loss of energy. |


Details
-------

To use a Physics Material 2D, simply drag it onto an object with a 2D collider attached or drag it to the collider component in the inspector. Note that for 3D physics, the equivalent asset is referred to as a _Physic Material_ (ie, no S at the end of _physic_) - it is important in scripting not to get the two spellings confused.
