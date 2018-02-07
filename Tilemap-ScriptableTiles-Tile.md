# Tile

The `Tile` class is a simple class that allows a sprite to be rendered on the Tilemap. Tile inherits from `TileBase`. The following is a description of the methods that are overridden to have the Tile’s behaviour.

```
public Sprite sprite;
public Color color = Color.white;
public Matrix4x4 transform = Matrix4x4.identity;
public GameObject gameobject = null;
public TileFlags flags = TileFlags.LockColor;
```

```
public ColliderType colliderType = ColliderType.Sprite;
```

These are the default properties of a Tile. If the Tile was created by dragging and dropping a Sprite onto the Tilemap Palette, the Tile would have the __Sprite__ property set as the sprite that was dropped in. You may adjust the properties of the Tile instance to get the Tile required.

```
public void RefreshTile(Vector3Int location, ITilemap tilemap)
```

This is not overridden from `TileBase`. By default, it only refreshes the Tile at that location.

```
public override void GetTileData(Vector3Int location, ITilemap tilemap, ref TileData tileData)
{
	tileData.sprite = this.sprite;
	tileData.color = this.color;
	tileData.transform = this.transform;
	tileData.gameobject = this.gameobject;
	tileData.flags = this.flags;

tileData.colliderType = this.colliderType;
}
```

This fills in the required information for Tilemap to render the Tile by copying the properties of the Tile instance into `tileData`.

```
public bool GetTileAnimationData(Vector3Int location, ITilemap tilemap, ref TileAnimationData tileAnimationData)
```

This is not overridden from TileBase. By default, the Tile class does not run any Tile animation and returns false.

```
public bool StartUp(Vector3Int location, ITilemap tilemap, GameObject go)
```

This is not overridden from `TileBase`. By default, the `Tile` class does not have any special start up functionality. If `tileData.gameobject` is set, the Tilemap still instantiates it on start up and place it at the location of the Tile.

---

* <span class="page-edit">2017-09-06 <!-- include IncludeTextNewPageSomeEdit --></span>