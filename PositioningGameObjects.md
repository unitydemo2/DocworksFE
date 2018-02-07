# Positioning GameObjects

To select a GameObject, click on it in the [Scene view](UsingTheSceneView) or click its name in the [Hierarchy window](Hierarchy). To select or de-select multiple GameObjects, hold the __Shift__ key while clicking, or drag a rectangle around multiple GameObjects to select them.

Selected GameObjects are highlighted in the Scene view. By default, this highlight is an orange outline around the GameObject; to change the highlight color and style, go to __Unity__ > __Preferences__ > __Color__ and edit the __Selected Wireframe__ and __Selected Outline__ colours. See documentation on the [Gizmo Menu](GizmosMenu) for more information about the outline and wireframe selection visualizations. The selected GameObjects also display a __Gizmo__ in the Scene view if you have one of the four Transform tools selected:

## Move, Rotate, Scale, and RectTransform

![](../uploads/Main/Editor-MoveRotateScaleTransform.png)

The first tool in the toolbar, the __Hand Tool__, is for panning around the Scene. The __Move__, __Rotate__, __Scale__, __Rect Transform__ and __Transform__ tools allow you to edit individual GameObjects. To alter the [Transform](class-Transform) component of the GameObject, use the mouse to manipulate any Gizmo axis, or type values directly into the number fields of the __Transform__ component in the Inspector.

Alternatively, you can select each of the four __Transform__ modes with a hotkey: __W__ for Move, __E__ for Rotate, __R__ for Scale, __T__ for RectTransform, and __Y__ for Transform.

![The Move, Scale, Rotate, Rect Transform and Transform Gizmos](../uploads/Main/MoveRotateScaleTransform.png)

### Move
At the center of the __Move__ Gizmo, there are three small squares you can use to drag the GameObject within a single plane (meaning you can move two axes at once while the third keeps still). 

If you hold shift while clicking and dragging in the center of the Move Gizmo, the center of the Gizmo changes to a flat square. The flat square indicates that you can move the GameObject around on a plane relative to the direction the Scene view Camera is facing.

### Rotate

With the __Rotate__ tool selected, change the GameObject's rotation by clicking and dragging the axes of the wireframe sphere Gizmo that appears around it. As with the Move Gizmo, the last axis you changed will be colored yellow. Think of the red, green and blue circles as performing rotation around the red, green and blue axes that appear in the Move mode (red is the x-axis, green in the y-axis, and blue is the z-axis). Finally, use the outermost circle to rotate the GameObject around the Scene view z-axis. Think of this as rotating in screen space.

### Scale

The __Scale__ tool lets you rescale the GameObject evenly on all axes at once by clicking and dragging on the cube at the center of the Gizmo. You can also scale the axes individually, but you should take care if you do this when there are child GameObjects, because the effect can look quite strange.

### RectTransform

The [RectTransform](class-RectTransform) is commonly used for positioning 2D elements such as Sprites or [UI elements](UIBasicLayout), but it can also be useful for manipulating 3D GameObjects. It combines moving, scaling and rotation into a single Gizmo:

* Click and drag within the rectangular Gizmo to move the GameObject. 
* Click and drag any corner or edge of the rectangular Gizmo to scale the GameObject. 
* Drag an edge to scale the GameObject along one axis. 
* Drag a corner to scale the GameObject on two axes. 
* To rotate the GameObject, position your cursor just beyond a corner of the rectangle. The cursor changes to display a rotation icon. Click and drag from this area to rotate the GameObject.

Note that in 2D mode, you can’t change the z-axis in the Scene using the Gizmos. However, it is useful for certain scripting techniques to use the z-axis for other purposes, so you can still set the z-axis using the Transform component in the Inspector.

For more information on transforming GameObjects, see documentation on the [Transform Component](class-Transform).

###Transform

The __Transform__ tool combines the __Move__, __Rotate__ and __Scale__ tools. Its Gizmo provides handles for movement and rotation. When the __Tool Handle Rotation__ is set to __Local__ (see below), the Transform tool also provides handles for scaling the selected GameObject.

## Gizmo handle position toggles

![](../uploads/Main/GizmoDisplayToggles.png)

The __Gizmo handle position toggles__ are used to define the location of any Transform tool Gizmo, and the handles use to manipulate the Gizmo itself.

![Gizmo display toggles](../uploads/Main/HandlePositionButtons.png)

### For position

Click the __Pivot__/__Center__ button on the left to toggle between __Pivot__ and __Center__.

* __Pivot__ positions the Gizmo at the actual pivot point of a Mesh.
* __Center__ positions the Gizmo at the center of the GameObject's rendered bounds.

### For rotation

Click the __Local__/__Global__ button on the right to toggle between __Local__ and __Global__.

* __Local__ keeps the Gizmo's rotation relative to the GameObject's.
* __Global__ clamps the Gizmo to world space orientation.

### Unit snapping

While dragging any Gizmo Axis using the __Move__ tool or the __Transform__ tool, hold the __Control__ key (__Command__ on Mac) to snap to increments defined in the __Snap Settings__ (menu:  __Edit__ > __Snap Settings...__)

![](../uploads/Main/SceneViewUnitSnappingSettings.png)

### Surface snapping

While dragging in the center using the __Move__ tool or the __Transform__ tool, hold __Shift__ and __Control__ (__Command__ on Mac) to quickly snap the GameObject to the intersection of any __Collider__.

### Look-at rotation

While using the __Rotate__ tool or the __Transform__ tool, hold __Shift__ and __Control__ (__Command__ on Mac) to rotate the GameObject towards a point on the surface of any __Collider__.

### Vertex snapping

Use __vertex snapping__ to quickly assemble your Scenes: take any vertex from a given Mesh and place that vertex in the same position as any vertex from any other Mesh you choose. For example, use vertex snapping to align road sections precisely in a racing game, or to position power-up items at the vertices of a Mesh.

Follow the steps below to use vertex snapping:

1. Select the Mesh you want to manipulate and make sure the __Move__ tool or the __Transform__ tool is active.

2. Press and hold the __V__ key to activate the vertex snapping mode.

3. Move your cursor over the vertex on your Mesh that you want to use as the pivot point.

4. Hold down the left mouse button once your cursor is over the vertex you want and drag your Mesh next to any other vertex on another Mesh.

5. Release the mouse button and the __V__ key when you are happy with the results (__Shift+V__ acts as a toggle of this functionality).

**Note:** You can snap vertex to vertex, vertex to surface, and pivot to vertex.

### Screen Space Transform

While using the __Transform__ tool, hold down the __Shift__ key to enable Screen Space mode. This mode allows you to move, rotate and scale GameObjects as they appear on the screen, rather than in the Scene. 

---

* <span class="page-history">Transform tool added in [2017.3](https://docs.unity3d.com/2017.3/Documentation/Manual/30_search.html?q=newin20173) <span class="search-words">NewIn20173</span></span>

* <span class="page-edit"> 2017-05-18  <!-- include IncludeTextAmendPageYesEdit --></span>