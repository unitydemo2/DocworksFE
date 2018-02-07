# Creating Tilemaps

From the __GameObject__ menu, move to __2D Object__ and select __Tilemap__.

This creates a new GameObject with a child GameObject in the scene. The GameObject is called __Grid__. The Grid GameObject determines the layout of child Tilemaps.

![](../uploads/Main/CreatingTilemaps-6.png)

The child GameObject is called __Tilemap__. It is comprised of a Tilemap component and Tilemap Renderer component. The Tilemap GameObject is where Tiles are painted on.

![](../uploads/Main/CreatingTilemaps-7.png)

To create additional Tilemaps to be used as  "layers", select the Grid GameObject or the Tilemap GameObject, and select __GameObject__ > __2D Object__ > __Tilemaps__ in the menu or right-click on the selected GameObject and click on __2D Object__ > __Tilemap__. 

![](../uploads/Main/CreatingTilemaps-8.png)

A new GameObject called __Tilemap (1)__ is added into the hierarchy of the selected GameObject. You can paint Tiles on this new GameObject as well.

![](../uploads/Main/CreatingTilemaps-9.png)

## Adjusting the Grid for Tilemaps

Select the Grid GameObject. Adjust the values in the Grid component in the inspector.

![](../uploads/Main/CreatingTilemaps-10.png)

| Property | Function |
|:--|:--|
| __Cell Size__ |Size of each cell in the Grid|
| __Cell Gap__ |Size of the Gap between each cell in the Grid|
| __Cell Swizzle__ |Swizzles the cell positions to other axes. For Example. In XZY mode, the Y and Z coordinates are swapped, so an input Y coordinate maps to Z instead and vice versa.|

Changes in the Grid affect all child Layer GameObjects with the Tilemap, Tilemap Renderer and Tilemap Collider 2D components.

---

* <span class="page-edit">2017-09-06 <!-- include IncludeTextNewPageSomeEdit --></span>
