#Building Height Mesh for Accurate Character Placement

Height mesh allows you to place your character more accurately on the walkable surfaces.

![](../uploads/Main/NavMeshHeightMesh.svg)

While navigating, the NavMesh Agent is constrained on the surface of the NavMesh. Since the NavMesh is an approximation of the walkable space, some features are evened out when the NavMesh is being built. For example, stairs may appear as a slope in the NavMesh. If your game requires accurate placement of the agent, you should enable _Height Mesh_ building when you bake the NavMesh. The setting can be found under the Advanced settings in Navigation window. Note that building Height Mesh will take up memory and processing at runtime, and it will take a little longer to bake the NavMesh.

###Further reading
- [Building a NavMesh](nav-BuildingNavMesh) – workflow for NavMesh baking.
