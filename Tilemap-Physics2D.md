# Tilemaps and Physics 2D

* You can add a Tilemap Collider 2D component to the GameObject of a Tilemap to generate a collider based on the Tiles of the Tilemap.

* A Tilemap Collider 2D component functions like a normal Collider 2D component. You can add Effector 2Ds to modify the behavior of the Tilemap Collider 2D. You can also composite the Tilemap Collider 2D with a [Composite Collider 2D](class-CompositeCollider2D).

* Adding or removing Tiles with __Collider Type__ set to __Sprite__ or __Grid__ adds or removes the Tile’s collider shape from the Tilemap Collider 2D component on the next `LateUpdate` for the Tilemap Collider 2D. This also happens when the Tilemap Collider 2D is being composited by a Composite Collider 2D.

---

* <span class="page-edit">2017-09-06 <!-- include IncludeTextNewPageSomeEdit --></span>