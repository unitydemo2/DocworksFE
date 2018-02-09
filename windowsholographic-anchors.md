#Anchors

Anchor components are a way for the virtual world to interact with the real world. An Anchor is a special component that overrides the position and orientation on the Transform component on the same GameObject. For GameObjects with an Anchor component, the system takes over and locks them in place in the real world, based on the system's understanding. For more information, see Microsoft's documentation on [WorldAnchors in Unity](https://dev.windows.com/en-us/holographic/world_anchor_in_unity).

##WorldAnchor

A World Anchor component represents a link between an exact point in the physical world and the parent GameObject of the World Anchor. Once added, a GameObject with a World Anchor component remains locked in place to locations in the real world. For example, a World Anchor could be used for:

* locking a holographic game board to the top of a table
* locking a video window to a wall

Use World Anchors wherever there's a GameObject or tree of GameObjects that you want to be fixed in a physical location.

World Anchors override their parent GameObject's Transform component, so any direct manipulations of the Transform component are lost. Similarly, GameObjects with World Anchor components should not contain Rigidbody components with __Dynamic__ physics. These components can be resource-intensive and affect game performance, so ensure that you use only a small number of Anchor components. For example, a game board surface placed upon a table only requires a single Anchor for the board; child GameObjects of the board do not require their own World Anchor.