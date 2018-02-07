#Creating a NavMesh Obstacle

NavMesh Obstacle components can be used to describe obstacles the agents should avoid while navigating. For example the agents should avoid physics controlled objects, such as crates and barrels while moving. 

We're going to add a crate to block the pathway at the top of the level.

![](../uploads/Main/NavMeshObstacleSetup.svg)

1. First create a **cube** to depict the crate: __Game Object &gt; 3D Object &gt; Cube__.
2. Move the cube to the platform at the top, the default size of the cube is good for a crate so leave it as it is.
3. Add a **NavMesh Obstacle component** to the cube. Choose **Add Component** from the inspector and choose **Navigation  &gt; NavMesh Obstacle**.
4. Set the shape of the obstacle to **box**, changing the shape will automatically fit the center and size to the render mesh.
5. Add a **Rigid body** to the obstacle. Choose **Add Component** from the inspector and choose **Physics &gt; Rigid Body**.
6. Finally turn on the **Carve** setting from the NavMesh Obstacle inspector so that the agent knows to find a path around the obstacle.

Now we have a working crate that is physics controlled, and which the AI knows how to avoid while navigating.

###Further Reading

- [Inner Workings of the Navigation System](nav-InnerWorkings) - learn more about how obstacles are used as part of navigation.
- [NavMesh Obstacle component reference](class-NavMeshObstacle) – full description of all the NavMesh Obstacle properties.
- [NavMesh Obstacle scripting reference](ScriptRef:AI.NavMeshObstacle.html) - full description of the NavMesh Obstacle scripting API.
