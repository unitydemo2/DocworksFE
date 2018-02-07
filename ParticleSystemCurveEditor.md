Particle System Curve Editor
============================

MinMax curves
-------------


Many of the properties in the particle system modules describe a change of a value with time. That change is described via __MinMax Curves__. 
These time-animated properties (for example __size__ and __speed__), will have a pull down menu on the right hand side, where you can choose between: 

![](../uploads/Main/MinMaxDropDown.png) 

__Constant__: The value of the property will not change with time, and will not be displayed in the __Curve Editor__

__Curve__: The value of the property will change with time based on the curve specified in the __Curve Editor__


![](../uploads/Main/ParticleSystemOneCurve.png) 
&gt;A property animated with a Curve

__Random between constants__: The value of the property will be selected at random between the two constants

__Random between curves__: A curve will be generated at random between the min and the max curve, and the value of the property will change in time based on the generated curve

![](../uploads/Main/BetweenTwoCurves.png) 
A property animated as __Random Between Two Curves__

In the __Curve Editor__, the _x_-axis spans time between 0 and the value specified by the __Duration__ property, and the _y_-axis represents the value of the animated property at each point in time. The range of the _y_-axis can be adjusted in the number field in the upper right corner of the __Curve Editor__. The __Curve Editor__ currently displays all of the curves for a particle system in the same window. 


![](../uploads/Main/ShurikenMultipleCurves.png) 
&gt;Multiple curves in the same curve editor

Note that the "-" in the bottom-right corner will remove the currently selected curve, while the "+" will _optimize_ it (that is make it into a parametrized curve with at most 3 keys). 

For animating properties that describe vectors in 3D space, we use the TripleMinMax Curves, which are simply curves for the x-,y-, and z- dimensions side by side, and it looks like this: 

![](../uploads/Main/ShurikenTripleMinMaxCurves.png) 

Managing many curves in the curve editor
----------------------------------------

To avoid cluttering in the __Curve Editor__, it is possible to toggle curves on and off, by clicking on them in the inspector. The Particle System Curve Editor can also be detached from the Inspector by right-clicking on the __Particle System Curves__ title bar, after which you should see something like this:


![](../uploads/Main/DetachedCurveEditor.png) 
A detached Curve Editor that can be docked like any other window 

For more information on working with curves, take a look at the [Curve Editor documentation](EditingCurves)
