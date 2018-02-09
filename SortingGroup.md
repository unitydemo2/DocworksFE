## Sorting Group

A Sorting Group is a component which alters the order in which [Sprite Renderers](class-SpriteRenderer) do their rendering. It allows a group of Renderers which share a common root to be sorted together. Renderers in Unity are sorted by several criteria, including their order in the layer and their distance from the Camera. 

### Setting up a Sorting Group

To use the Sorting Group component, add it to the [GameObject’s](class-GameObject) root (the parent GameObject of all the GameObjects you want to apply group sorting to). Select the GameObject’s root, then in the main menu select __Component__ > __Rendering__ > __Sorting Group__.

A Sorting Group does not have any visual representation in the Scene view. It can be added to an empty GameObject, which might be useful if you have many GameObjects to apply group sorting to at once. 

A Sorting Group is not dependent on any other Renderers, and any Renderers that are attached to that GameObject and its descendants are rendered together.

![The Sorting Group component](../uploads/Main/SortingGroup-0.png)

| **Property** | **Function** |
|:---|:---| 
| __Sorting Layer__ | Use the drop-down to select the Layer used to define this Sprite’s overlay priority during rendering. |
| __Order in Layer__ | Set the overlay priority of this Sprite within its layer. Lower numbers are rendered first, and subsequent numbers overlay those below. |

### Sorting a Sorting Group

Unity uses the concept of sorting layers to allow you to divide sprites into groups for overlay priority. Sorting Groups with a __Sorting Layer__ lower in the order are overlaid by those in a higher __Sorting Layer__.

Sometimes, two or more objects in the same __Sorting Layer__ can overlap (for example, two player characters in a side scrolling game, as shown in the example below). The __Order in Layer__ property can be used to apply consistent priorities to Sorting Groups in the same layer. As with __Sorting Layer__, lower numbers are rendered first, and are obscured by Sorting Groups with higher layer numbers, which are rendered later. See the documentation on [Tags and Layers](class-TagManager) for details on editing __Sorting Layers__. 

The descendants of the Sorting Group are sorted against other descendants of closest or next Sorting Group (depending on whether sorting is by distance or Order in Layer). In other words, the Sorting Group creates a local sorting space for its descendants only. This allows each of the Renderers inside the group to be sorted using the __Sorting Layer__ and __Order in Layer__, but locally to the containing Sorting Group.

### Nested Sorting Group

A nested Sorting Group is sorted against other Renderers in the same group.

However, GameObjects in the Hierarchy that do not have a Sorting Group are rendered together as a single layer, and Renderers are still sorted based on their __Sorting Layer__ and __Order in Layer__. 

**Example of how to use Sorting Groups**

Sorting Groups are commonly used in 2D games with complex characters, made up of several Sprites. This example uses a 2D character with multiple Renderers in a Hierarchy. 

![A character made up of several Sprites in a single Sorting Layer, using multiple __Order in Layers__ to sort its body parts](../uploads/Main/SortingGroup-1.png)

This character is in a single Sorting Layer, and uses multiple __Order in Layers__ to sort its body parts. Unity then saves the character as a [Prefab](Prefabs), and clones it multiple times during gameplay. 

When cloned, the body parts overlap each other because they are on the same layers, as seen below.

![The body parts of two characters overlap, because they share the same layers](../uploads/Main/SortingGroup-2.png)

The desired outcome is to have all the Renderers of one character render together, and then be followed by the next character. This gives the visual effect of passing each other, with one appearing closer to the camera than the other, rather than both of them appearing to blend together.

A Sorting Group component added to the root of the character ensures that the body parts no longer overlap and mix together. 

![The Sorting Group component sorts each character as a group, preventing the issue of overlapping body parts](../uploads/Main/SortingGroup-3.png)

![Multiple characters being sorted using a Sorting Group component on each character](../uploads/Main/SortingGroup-4.png)
