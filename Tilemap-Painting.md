# Painting Tilemaps

To paint on a Tilemap it must be the selected Active Tilemap in the Tile Palette. Tilemaps in the Scene are automatically added to the list.

![](../uploads/Main/Tilemap-Painting-13.png)

The Tile painting tools are found on the Tilemap Palette

![](../uploads/Main/Tilemap-Painting-14.png)

Click on the __Paint Tool__ icon, select a Tile from the Tilemap Palette and Left-click on the Tilemap in the Scene View to start laying out Tiles.

![The __Paint Tool__](../uploads/Main/Tilemap-Painting-16.png)

A selection of Tiles can be painted with the Paint Tool. Left-click and drag in the Tilemap Palette to make a selection.

![](../uploads/Main/Tilemap-Painting-17.png)

Holding Shift while using the Paint Tool toggles the Erase Tool.

![](../uploads/Main/Tilemap-Painting-18.png)

The __Rectangle Tool__ draws a rectangular shape on the Tilemap and fills it with the selected tiles.

![The __Rectangle Tool__](../uploads/Main/Tilemap-Painting-20.png)

The __Picker Tool__ is used to pick Tiles from the Tilemap to paint with. Left-click and drag to select multiple Tiles. Hold the __Ctrl__ key (or __Cmd__ on macOS) while in __Paint Tool__ mode to toggle the __Picker Tool__. 

![The __Picker Tool__](../uploads/Main/Tilemap-Painting-22.png)

The __Fill Tool__ is used to fill an area of Tiles with the selected Tile.

![The __Fill Tool__](../uploads/Main/Tilemap-Painting-24.png)

![](../uploads/Main/Tilemap-Painting-25.png)

The __Select Tool__ is used to select an area of Tiles to be inspected.

![The __Select Tool__](../uploads/Main/Tilemap-Painting-27.png)

The __Move Tool__ is used to move a selected area of tiles to another position. Click and drag the selected area to move the Tiles.

![The __Move Tool__](../uploads/Main/Tilemap-Painting-29.png)



## Tilemap Focus mode

If you have many Tilemap layers but would like to work solely on a specific layer to work on, you can focus on that particular layer and block out all other GameObject from view.

![](../uploads/Main/Tilemap-Painting-30.png)

Select the target Tilemap GameObject from the Active Target dropdown in the Palette window or from the Hierarchy window. In the bottom right corner of the SceneView, there is a Tilemap overlay window.

Change the __Focus On__ target in the dropdown:

* __None__ - No GameObject is focused.
* __Tilemap__ - The target Tilemap GameObject is focused. All other GameObjects are faded away. This is good if you want to focus on a single Tilemap layer.
* __Grid__ - The parent Grid GameObject with all its children is focused. All other GameObjects are faded away. This is good if you want to focus on the entire Tilemap as a whole.

---

* <span class="page-edit">2017-09-06 <!-- include IncludeTextNewPageSomeEdit --></span>
