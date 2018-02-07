# Scriptable Tiles

##Creating Scriptable Tiles

Create a new class inheriting from `TileBase` (or any useful sub-classes of `TileBase`, like `Tile`). Override any required methods for your new `Tile` class. The following are the usual methods you would override:

* `RefreshTile` determines which Tiles in the vicinity are updated when this Tile is added to the Tilemap. 
* `GetTileData` determines what the Tile looks like on the Tilemap.

Create instances of your new class using `ScriptableObject.CreateInstance<(Your Tile Class>()`. You may convert this new instance to an Asset in the Editor in order to use it repeatedly by calling `AssetDatabase.CreateAsset()`.

You can also make a custom editor for your Tile. This works the same way as custom editors for scriptable objects.

Remember to save your project to ensure that your new Tile Assets are saved!

---

* <span class="page-edit">2017-09-06 <!-- include IncludeTextNewPageSomeEdit --></span>

