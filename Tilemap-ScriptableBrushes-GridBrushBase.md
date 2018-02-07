# GridBrushBase

All brushes added must inherit from `GridBrushBase`. `GridBrushBase` provides a fixed set of APIs for painting. 

```
public virtual void Paint(GridLayout grid, GameObject brushTarget, Vector3Int position)
```

`Paint` adds data onto the target GameObject `brushTarget` with the `GridLayout` grid at the given position. This is triggered when the Brush is activated on the grid and the __Paint Tool__ is selected on the Palette window. Override this to implement the action desired on painting.

```
public virtual void Erase(GridLayout grid, GameObject brushTarget, Vector3Int position)
```

`Erase` removes data onto the target GameObject `brushTarget` with the `GridLayout` grid at the given position. This is triggered when the Brush is activated on the grid and the __Erase Tool__ is selected on the Palette window. Override this to implement the action desired on erasing.

```
public virtual void BoxFill(GridLayout grid, GameObject brushTarget, BoundsInt position)
```

`BoxFill` adds data onto the target GameObject `brushTarget` with the `GridLayout` grid onto the given bounds. This is triggered when the Brush is activated on the grid and the __Box Fill Tool__ is selected on the Palette window. Override this to implement the action desired on filling.

```
public virtual void FloodFill(GridLayout grid, GameObject brushTarget, Vector3Int position)
```

`FloodFill` adds data onto the target GameObject `brushTarget` with the `GridLayout` grid starting at the given position and filling all other possible areas linked to the position. This is triggered when the Brush is activated on the grid and the __Flood Fill Tool__ is selected on the Palette window. Override this to implement the action desired on filling.

```
public virtual void Rotate(RotationDirection direction)
```

`Rotate` rotates the content in the brush with the given direction based on the currently set pivot. 

```
public virtual void Flip(FlipAxis flip)
```

`Flip` flips the content of the brush with the given axis based on the currently set pivot.

```
public virtual void Select(GridLayout grid, GameObject brushTarget, BoundsInt position)
```

`Select` marks a boundary on the target GameObject `brushTarget` with the `GridLayout` grid from the given bounds. This allows you to view information based on the selected boundary and move the selection with the __Move Tool__. This is triggered when the Brush is activated on the grid and the Select tool is selected on the Palette window. Override this to implement the action desired when selecting from a target.

```
public virtual void Pick(GridLayout grid, GameObject brushTarget, BoundsInt position, Vector3Int pivot)
```

`Pick` pulls data from the target GameObject `brushTarget` with the `GridLayout` grid from the given bounds and pivot position, and fills the brush with that data. This is triggered when the Brush is activated on the grid and the __Pick Tool__ is selected on the Palette window. Override this to implement the action desired when picking from a target.

```
public virtual void Move(GridLayout grid, GameObject brushTarget, BoundsInt from, BoundsInt to)
```

`Move` marks the movement from the target GameObject `brushTarget` with the `GridLayout` grid from the given starting position to the given ending position. Override this to implement the action desired when moving from a target. This is triggered when the Brush is activated on the grid and the __Move Tool__ is selected on the Palette window and the Move is performed (`MouseDrag`). Generally, this would be any behaviour while a `Move` operation from the brush is being performed.

```
public virtual void MoveStart(GridLayout grid, GameObject brushTarget, BoundsInt position)
```

`MoveStart` marks the start of a move from the target GameObject `brushTarget` with the `GridLayout` grid from the given bounds. This is triggered when the Brush is activated on the grid and the __Move Tool__ is selected on the Palette window and the `Move` is first triggered (`MouseDown`). Override this to implement the action desired when starting a move from a target. Generally, this would be picking of data from the target with the given start position.

```
public virtual void MoveEnd(GridLayout grid, GameObject brushTarget, BoundsInt position)
```

`MoveEnd` marks the end of a move from the target GameObject `brushTarget` with the `GridLayout` grid from the given bounds. This is triggered when the Brush is activated on the grid and the __Move Tool__ is selected on the Palette window and the `Move` is completed (`MouseUp`). Override this to implement the action desired when ending a move from a target. Generally, this would be painting of data to the target with the given end position.

---

* <span class="page-edit">2017-09-06 <!-- include IncludeTextNewPageSomeEdit --></span>