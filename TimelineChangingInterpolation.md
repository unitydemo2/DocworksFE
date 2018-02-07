### Changing interpolation and shape

Every key has one or two tangents that control the interpolation of the animation curve. The term __interpolation__ refers to the estimation of values that determine the shape of the animation curve between two keys.

Whether a key has one of two tangents depends on the location of the key on the animation curve. The first key has only a right tangent that controls the interpolation of the animation curve after the key. The last key has only a left tangent that controls the interpolation of the animation curve before the last key. 

![The first key (red) has only a right tangent, and the last key (blue) has only a left tangent](../uploads/Main/timeline_curves_first_last_tangent.png)

All other keys have two tangents where the left tangent controls the interpolation before the key, and the right tangent controls the interpolation after the key. By default, tangents are joined. Dragging one tangent affects the position of both tangents, and the interpolation of the animation curve both before and after the key. 

![Keys that are neither the first key nor last key have joined tangents by default. Dragging either tangent changes the interpolation of the animation curve both before and after the key.](../uploads/Main/timeline_curves_tangent_joined.png)

Dragging a tangent may also change the interpolation mode of the animation curve. For example, most keys are set to the Clamped Auto interpolation mode which automatically smooths animation curve as it passes through the key. If you drag a tangent of a key set to Clamped Auto, the interpolation mode changes to Free Smooth.

The term __interpolation mode__ refers to the interpolation algorithm that determines which shape to use when drawing the animation curve.  

To view the interpolation mode for a key, select the key and Right-click. The context menu shows the interpolation mode. To change the interpolation mode for a key, select the key, Right-click and select another interpolation mode.

![The context menu shows the interpolation mode for the selected key. Use the context menu to change the interpolation mode.](../uploads/Main/timeline_curves_interp_menu.png)

Some interpolation modes break the left and right tangents so that they can be positioned separately. When tangents are broken, you can set a separate interpolation mode for the animation curve before the key and the animation curve after the key. For more details on the different interpolation modes, see [Editing Curves](EditingCurves). In the [Animation window documentation](AnimationEditorGuide), the interpolation mode is referred to as __tangent type__.

---
* <span class="page-edit">2017-08-10  <!-- include IncludeTextNewPageSomeEdit --></span>
