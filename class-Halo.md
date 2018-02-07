#Halo

__Halos__ are light areas around light sources, used to give the impression of small dust particles in the air. 


##Properties
![](../uploads/Main/Inspector-Halo.png)


|**_Property:_** |**_Function:_** |
|:---|:---|
|__Color__ |Color of the Halo. |
|__Size__ |Size of the Halo. |

##Details

You can add a Halo component to a [Light](class-Light) object and then set its size and color properties to give the desired glowing effect. A Light component can also be set to  display a halo without a separate Halo component by enabling its _Draw Halo_ property.

##Hints

* To see Halos in the scene view, check __Fx__ button in the __Scene View__ Toolbar.
* To override the shader used for Halos copy the Internal-Halo.shader shader from the [Built-in shaders](http://unity3d.com/support/resources/assets/built-in-shaders) into a folder named "Resources" in your "Assets" folder.

![A Light with a separate Halo __Component__](../uploads/Main/HaloWindow.png) 
