# TileBase

All tiles to be added to the Tilemap must inherit from `TileBase`. `TileBase` provides a fixed set of APIs to the Tilemap to communicate its rendering properties. For most cases of the APIs, the location of the Tile and the instance of the Tilemap the Tile is placed on is passed in as arguments of the API. You may use this to determine any required attributes for setting the tile information.

```
public void RefreshTile(Vector3Int location, ITilemap tilemap)
```

`RefreshTile` determines which Tiles in the vicinity are updated as this Tile is added to the Tilemap. By default, the `TileBase` calls `tilemap.RefreshTile(location)` to refresh the tile at the current location. Override this to determine which Tiles need to be refreshed due to the placement of the new Tile. 

**Example:** There is a straight road, and you place a `RoadTile` next to it. The straight road isn’t valid anymore. It needs a T-section instead. Unity doesn’t automatically know what needs to be refreshed, so `RoadTile` needs to trigger the refresh onto itself, but also onto the neighboring road.

```
public bool GetTileData(Vector3Int location, ITilemap tilemap, ref TileData tileData)
```

`GetTileData` determines what the Tile looks like on the Tilemap. See `TileData` below for more details.

```
public bool GetTileAnimationData(Vector3Int location, ITilemap tilemap, ref TileAnimationData tileAnimationData)
```

`GetTileAnimationData` determines whether or not the Tile is animated. Return true if there is an animation for the Tile, other returns false if there is not.

```
public bool StartUp(Vector3Int location, ITilemap tilemap, GameObject go)
```

`StartUp` is called for each tile when the Tilemap updates for the first time. You can run any start up logic for Tiles on the Tilemap if necessary. The argument *go* is the instanced version of the object passed in as gameobject when `GetTileData` was called. You may update *go* as necessary as well.

---

* <span class="page-edit">2017-09-06 <!-- include IncludeTextNewPageSomeEdit --></span>