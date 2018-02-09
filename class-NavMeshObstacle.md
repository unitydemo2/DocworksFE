# Nav Mesh Obstacle

The __Nav Mesh Obstacle__ component allows you to describe moving obstacles that [Nav Mesh Agents](class-NavMeshAgent) should avoid while navigating the world (for example, barrels or crates controlled by the physics system). While the obstacle is moving, the Nav Mesh Agents do their best to avoid it. When the obstacle is stationary, it carves a hole in the NavMesh. Nav Mesh Agents then change their paths to steer around it, or find a different route if the obstacle causes the pathway to be completely blocked.

![](../uploads/Main/NavMeshObstacle.png)

| **Property**| **Function** |
|:---|:---| 
| __Shape__| The shape of the obstacle geometry. Choose whichever one best fits the shape of the object. |
|&nbsp;&nbsp;&nbsp;&nbsp;__Box__|  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Center| Center of the box relative to the transform position. |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Size| Size of the box. |
| &nbsp;&nbsp;&nbsp;&nbsp;__Capsule__|  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Center| Center of the capsule relative to the transform position. |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Radius| Radius of the capsule. |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Height| Height of the capsule. |
| __Carve__| When the Carve checkbox is ticked, the Nav Mesh Obstacle creates a hole in the NavMesh. |
| &nbsp;&nbsp;&nbsp;&nbsp;Move Threshold| Unity treats the Nav Mesh Obstacle as moving when it has moved more than the distance set by the Move Threshold. Use this property to set the threshold distance for updating a moving carved hole. |
| &nbsp;&nbsp;&nbsp;&nbsp;Time To Stationary| The time (in seconds) to wait until the obstacle is treated as stationary. |
| &nbsp;&nbsp;&nbsp;&nbsp;Carve Only Stationary| When enabled, the obstacle is carved only when it is stationary. See [Logic for moving Nav Mesh Obstacles](#LogicMovingObstacles), below, to learn more. |

## __Details__

![](../uploads/Main/NavMeshObstacleCarving.svg)

Nav Mesh Obstacles can affect the Nav Mesh Agent’s navigation during the game in two ways:

### Obstructing

When __Carve__ is not enabled, the default behavior of the Nav Mesh Obstacle is similar to that of a Collider. Nav Mesh Agents try to avoid collisions with the Nav Mesh Obstacle, and when close, they collide with the Nav Mesh Obstacle. Obstacle avoidance behaviour is very basic, and has a short radius. As such, the Nav Mesh Agent might not be able to find its way around in an environment cluttered with Nav Mesh Obstacles. This mode is best used in cases where the obstacle is constantly moving (for example, a vehicle or player character).

### Carving

When __Carve__ is enabled, the obstacle carves a hole in the NavMesh when stationary. When moving, the obstacle is an obstruction. When a hole is carved into the NavMesh, the pathfinder is able to navigate the Nav Mesh Agent around locations cluttered with obstacles, or find another route if the current path gets blocked by an obstacle. It’s good practice to turn on carving for Nav Mesh Obstacles that generally block navigation but can be moved by the player or other game events like explosions (for example, crates or barrels).

![](../uploads/Main/NavMeshObstacleTrap.svg)

<a name="LogicMovingObstacles"> </a>

## Logic for moving Nav Mesh Obstacles

Unity treats the Nav Mesh Obstacle as moving when it has moved more than the distance set by the __Carve__ > __Move Threshold__. When the Nav Mesh Obstacle moves, the carved hole also moves. However, to reduce CPU overhead, the hole is only recalculated when necessary. The result of this calculation is available in the next frame update. The recalculation logic has two options:

* Only carve when the Nav Mesh Obstacle is stationary

* Carve when the Nav Mesh Obstacle has moved

###Only carve when the Nav Mesh Obstacle is stationary

This is the default behavior. To enable it, tick the Nav Mesh Obstacle component’s __Carve Only Stationary__ checkbox. In this mode, when the Nav Mesh Obstacle moves, the carved hole is removed. When the Nav Mesh Obstacle has stopped moving and has been stationary for more than the time set by __Carving Time To Stationary__, it is treated as stationary and the carved hole is updated again. While the Nav Mesh Obstacle is moving, the Nav Mesh Agents avoid it using collision avoidance, but don’t plan paths around it. 

__Carve Only Stationery__ is generally the best choice in terms of performance, and is a good match when the GameObject associated with the Nav Mesh Obstacle is controlled by physics.

###Carve when the Nav Mesh Obstacle has moved

To enable this mode, untick the Nav Mesh Obstacle component’s __Carve Only Stationary__ checkbox. When this is unticked, the carved hole is updated when the obstacle has moved more than the distance set by __Carving Move Threshold__. This mode is useful for large, slowly moving obstacles (for example, a tank that is being avoided by infantry).

**Note**: When using NavMesh query methods, you should take into account that there is a one-frame delay between changing a Nav Mesh Obstacle and the effect that change has on the NavMesh.

## See also

1. [Creating a Nav Mesh Obstacle](http://mdeditor.infra.hq.unity3d.com/#nav-CreateNavMeshObstacle) - Guidance on creating Nav Mesh Obstacles.

2. [Inner Workings of the Navigation System](http://nav-innerworkings) - Learn more about how Nav Mesh Obstacles are used as part of navigation.

3. [Nav Mesh Obstacle scripting reference](ScriptRef:AI.NavMeshObstacle) - Full description of the Nav Mesh Obstacle scripting API.

