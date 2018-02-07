Selecting a Root Motion Node
===================================================

When root motion is contained within an imported animation clip, that motion will be used to drive the movement and rotation of the GameObject that is playing the animation. Sometimes however it may be necessary to manually select a different specific node within the hierarchy of your animation file to act as the root motion node.

(example use case required here)

The Motion field within the Animation import settings allows you to use a hierarchical popup menu to select any node (Transform) within the hierarchy of the imported animation and use it as the root motion source. That object's animated position and rotation will control the animated position and rotation of the GameObject playing back the animation.

To select a root motion node for an animation, first select the imported animation file in your project view, then in the import settings in the inspector, select the Animations button.

![View the Animations section of the Import Settings for your animation file](../uploads/Main/FBXImporterInspectorAnimationsSection.png) 

Then scroll all the way to the bottom of the inspector to find the Motion heading, among the four fold-out headings as shown:

![The Motion fold-out heading, along with the Mask, Curves, and Events headings](../uploads/Main/AnimationInspectorMasksCurvesEventsMotion.png) 

Expand the motion heading to reveal the Root Motion Node menu. When you open the menu, you'll see the options * None *, * Root Transform *, and any objects that are in the root of the imported file's hierarchy. This may be your character's mesh objects, as well as its root bone name, and a submenu for each item that has child objects. Each submenu also contains the child object(s) itself, and further sub-menus if / those / objects have child objects.

![Traversing the hierarchy of objects to select a root motion node](../uploads/Main/AnimationInspectorRootNodeSelectionMenu.png) 

Once the Root motion node has been selected, the object's motion will now be driven by the animation from that particular object.


