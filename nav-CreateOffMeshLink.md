#Creating an Off-mesh Link

Off-Mesh Links are used to create paths crossing outside the walkable navigation mesh surface. For example, jumping over a ditch or a fence, or opening a door before walking through it, can be all described as Off-mesh links.

We're going to add an Off-Mesh Link component to describe a jump from the upper platform to the ground.

![](../uploads/Main/OffMeshLinkSetup.svg)  

1. First create **two cylinders**: __Game Object &gt; 3D Object &gt; cylinder__.
2. You can scale the cylinders to _(0.1, 0.5, 0.1)_ to make it easier to work with them.
3. Move the **first cylinder** at the edge of the top platform, close to the NavMesh surface.
4. Place the **second cylinder** on the ground, close to the NavMesh, at the location where the link should land.
5. Select the cylinder on the left and add an Off-Mesh Link component to it. Choose **Add Component** from the inspector and choose **Navigation &gt; Off Mesh Link**.
6. Assign the leftmost cylinder in the **Start** field and rightmost cylinder in the **End** field.

Now you have functioning Off-Mesh Link set up! If the path via the off-mesh link is shorter than via walking along the Navmesh, the off-mesh link will be used.

You can use any game object in the scene to hold the Off-Mesh link component, for example a fence prefab could contain the off-mesh link component. Similarly you can use any game object with a Transform as the start and end marker.

The NavMesh bake process can detect and create common jump-across and drop-down links automatically. Take a look at the [Building Off-Mesh Links Automatically](nav-BuildingOffMeshLinksAutomatically) for more details.

###Further Reading

- [Building Off-Mesh Links Automatically](nav-BuildingOffMeshLinksAutomatically) - learn how to automatically build Off-Mesh Links.
- [Navigation HowTos](nav-HowTos) - common use cases for NavMesh Agent, with source code.
- [Off-Mesh Link component reference](class-OffMeshLink) – full description of all the Off-Mesh Link properties.
- [Off-Mesh Link scripting reference](ScriptRef:AI.OffMeshLink.html) - full description of the Off-Mesh Link scripting API.
