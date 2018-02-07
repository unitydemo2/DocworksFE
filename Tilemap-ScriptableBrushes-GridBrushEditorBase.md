# GridBrushEditorBase

All brush editors added must inherit from `GridBrushEditorBase`. `GridBrushEditorBase` provides a fixed set of APIs for drawing of inspectors on the Palette window and drawing of Gizmos on the Scene View. 

```
public virtual GameObject[] validTargets
```

This returns a list of GameObjects which are valid targets to be painted on by the brush. This appears in the dropdown in the Palette window. Override this to have a custom list of targets which this Brush can interact with.

```
public virtual void OnPaintInspectorGUI()
```

This displays an inspector for editing Brush options in the Palette. Use this to update brush functionality while editing in the Scene view.

```
public virtual void OnSelectionInspectorGUI()
```

This displays an inspector for when cells are selected on a target Grid. Override this to show a custom inspector view for the selected cells.

```
public virtual void OnPaintSceneGUI(GridLayout grid, GameObject brushTarget, BoundsInt position, GridBrushBase.Tool tool, bool executing)
```

This is used for drawing additional gizmos on the Scene View when painting with the brush. Tool is the currently selected tool in the Palette. Executing returns whether the brush is being used at the particular time.

---

* <span class="page-edit">2017-09-06 <!-- include IncludeTextNewPageSomeEdit --></span>