# Sprite Editor: Edit Outline

Use the [Sprite Editor’s](SpriteEditor) __Edit Outline__ option to edit the generated [Mesh](class-Mesh) for a [Sprite](Sprites), effectively editing its outline. 

Transparent areas in a Sprite can negatively affect your project’s performance. This feature is useful for fine-tuning the bounds of a Sprite, ensuring there are fewer transparent areas in the shape.
 
To access this option, select the Sprite and open the [Sprite Editor](SpriteEditor) (click __Sprite Editor__ in the Inspector window). Click the __Sprite Editor__ drop-down in the top left, and select __Edit Outline__. 

![Use the Sprite Editor’s drop-down to access __Edit Outline__](../uploads/Main/SpriteEditor0.png)

With __Edit Outline__ selected, click a Sprite. The Sprite Editor displays the outline and control points of the Sprite. The outline is indicated by a white line. The control points are areas you can use to move and manipulate the outline. Control points are indicated by small squares. Click and drag a white square outline control point to change its position.

![The white squares represent the outline control points - click and drag to change their positions](../uploads/Main/SpriteEditor1.png)

When you hover the mouse over a white square outline control point, a blue square appears on the outline. Drag this to reposition the control point and the blue square becomes a new white square outline control point, as shown below

![Hover over a white square control point, then drag the blue square to the position you want the new control point](../uploads/Main/SpriteEditor2.png)

To create new outlines, drag in an empty space within the Sprite. This creates a new rectangular outline with four control points. Do this multiple times to create multiple outlines on one Sprite (for example, a donut Sprite which has gaps inside the outline).

![Create new outlines by dragging in an empty space within the Sprite - you can use multiple outlines in one Sprite](../uploads/Main/SpriteEditor3.png)

To move the outline instead of the control points, hold __Ctrl__ while you click and drag the outline.

![Hold __Ctrl__ to drag the line (here shown in yellow) rather than the control points.](../uploads/Main/SpriteEditor4.png)

## Outline Tolerance
Use the __Outline Tolerance__ slider to increase and decrease the number of outline control points available, between __0__ (the minimum number of control points) and __1__ (the maximum number of control points). A higher __Outline Tolerance__ creates more outline control points, while a lower __Outline Tolerance__ creates a tighter Mesh (that is, a Mesh with a smaller border of transparent pixels between the Sprite and the Mesh edges). Click __Update__ to apply the change.

![Use the __Outline Tolerance__ slider to determine the number of control points](../uploads/Main/SpriteEditor5.png)

![The Sprite on the left has a low __Outline Tolerance__, and the Sprite on the right has a high __Outline Tolerance__](../uploads/Main/SpriteEditor6.png)
