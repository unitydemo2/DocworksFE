Network Proximity Checker
=========================

The NetworkProximityChecker is a component that can be used to control the visibility of objects for network clients, based on proximity to network players. To use it, put the component on the object that should be visible within a certain range. This class relies on physics to calculate visibility.

Properties
----------

|**_Property:_** ||**_Function:_** |
|:---|:---|:---|
|__visRange__ ||The range that the object should be visible in. |
|__visUpdateInterval__ ||how often in seconds the object should check for players entering it's visible range. |
|__checkMethod__ ||Which type of physics to use for proximity checking. |

