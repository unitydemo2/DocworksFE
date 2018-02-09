# The Look Dev view

The Look Dev view is the main window. You can open multiple Look Dev views at once.

By default there is only one view in the Look Dev view, but you can choose from a selection of split-screen views. See [Multi-view](#MultiView) below to learn more about this.

## Loading Prefabs into the Look Dev view

The Look Dev view is primarily designed to view Asset Prefabs.

To load a Prefab into the Look Dev view, right click the Prefab and select __Open in Look Dev Tool__. Alternatively, if Look Dev is already open, drag and drop the Prefab from the Hierarchy window directly into the Look Dev view.

**Note:** When you right click on a Prefab to load it into Look Dev, it automatically loads into the currently visible Look Dev view or the last active one.

<a name="MultiView"></a>
## Multi-view

By default, the Look Dev view displays a single pane containing the Prefab you are working with. Use the buttons in the [Control Panel](LookDevControlPanel) to display a split-screen duplicate pane alongside it, allowing you to compare and contrast different settings. 

![Control panel](../uploads/Main/LookDevControlPanel.png)

When you select the button containing the number __1__ or number __2__ , the Look Dev view is in single-pane mode. Each button corresponds to its view in Look Dev. Select button __1__ to apply settings to view 1, and button __2__ to apply settings to view 2. The other three buttons are as follows:

__Side-by-side__: ![](../uploads/Main/LookDevView-SideBySideButton.png)

Duplicate views displayed side by side.

![__Side-by-side__ view](../uploads/Main/LookDevView-SideBySide.jpg)

By default, both views use the same camera. The lock button ![](../uploads/Main/LookDevView-LockButton.png) at the center decouples this behavior, allowing you to manipulate the camera in both views independently.

__Split-screen__: ![](../uploads/Main/LookDevView-SplitScreenButton.png)

The view is split horizontally in two, and an orange/blue manipulation Gizmo represents the separation plane between the two views (see [Using the manipulation Gizmo](#UsingGizmo) below for guidance on using this).

![__Split-screen__ view](../uploads/Main/LookDevView-Gizmo.png)

__Zone__ ![](../uploads/Main/LookDevView-ZoneButton.png)

The view is split in two, with a circular split defined by the position of the orange/blue manipulation Gizmo:

![__Zone__ view](../uploads/Main/LookDevView-Zone.png)

To load a different Prefab into each split-screen view, go to __Settings__ and enable __Allow Different Objects__, then drag and drop each Prefab into its intended view. 

Note that in multi-view modes, it only makes sense to do this if you need to look at two different versions of the same Asset. Comparing completely different Assets doesn’t give you a good idea of the difference in lighting or visual effect.

<a name="UsingGizmo"></a>
## Using the manipulation Gizmo

The manipulation Gizmo has different behaviour in Split-screen and Zone modes, but you use it in the same way in both.

###Moving the separator
To move the separator, click on the narrow part of the Gizmo and drag and drop it to the location you want.

![Click, drag and drop to move the separation pane](../uploads/Main/LookDevView-GizmoBefore.png)

![The separation plane dragged to the right ](../uploads/Main/LookDevView-GizmoAfter.png)

###Changing the orientation and length
To change the orientation and length of the manipulator Gizmo, click and drag the circle at either end of the manipulator.

In Zone mode, moving the circles on the manipulator Gizmo changes the radius of the view circle.

![How to move the circles on the manipulator Gizmo](../uploads/Main/LookDevView-GizmoZoneBefore.png) 

![Moving the Gizmo circles has made a larger radius of the view circle ](../uploads/Main/LookDevView-GizmoZoneAfter.png)

###Changing the separation in increments
To change the separation in increments, click and hold the circle on the end of the manipulation Gizmo, then hold __Shift__ as you move the mouse. This snaps the manipulation Gizmo to set angles, which is useful for a perfectly horizontal, vertical or diagonal angle.

The central white circle on the separator allows you to blend between the two views. Left click on it and drag it along the orange line to blend the left-hand view with the right-hand view (as shown in Image A below). Drag to the blue line to blend the right-hand view with the left-hand view (as shown in Image B below).

![Image A](../uploads/Main/LookDevView-GizmoIncrementBefore.png) 

![Image B](../uploads/Main/LookDevView-GizmoIncrementAfter.png)

The white circle automatically snaps back into the center when you drag it back. This helps you get back to the default blending value quickly.

##Uses for each option

* __Side-by-side__: Compare two different lighting conditions on the same Asset to check that it behaves correctly.

* __Split-screen/Zone__: Investigate texture problems using a debug Shader mode (for example, use one screen to view Normal or Albedo shading, and the environment-lit mode on the other).

* __Side-by-side/Split-screen/Zone__: Compare two different versions of the same Asset using the same lighting conditions to see which changes improve the Asset’s quality.

* __Side-by-side/Split-screen/Zone__: Compare two different [Asset LODs](LevelOfDetail) using the same lighting conditions, to test the quality of the LOD.