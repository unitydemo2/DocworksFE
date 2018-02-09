#Mesh Filter

The __Mesh Filter__ takes a mesh from your assets and passes it to the [Mesh Renderer](class-MeshRenderer) for rendering on the screen.

![](../uploads/Main/Inspector-MeshFilter.png) 



##Properties

|**_Property:_** |**_Function:_** |
|:---|:---|
|__Mesh__ |Reference to a [mesh](class-Mesh) that will be rendered. The __Mesh__ is located inside your Assets Directory. |


##Details

When importing mesh assets, Unity automatically creates a [Skinned Mesh Renderer](class-SkinnedMeshRenderer) if the mesh is skinned, or a Mesh Filter along with a Mesh Renderer, if it is not.

To see the Mesh in your scene, add a [Mesh Renderer](class-MeshRenderer) to the GameObject. It should be added automatically, but you will have to manually re-add it if you remove it from your object. If the Mesh Renderer is not present, the Mesh will still exist in your scene (and computer memory) but it will not be drawn.

