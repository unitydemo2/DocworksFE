# Scriptable Brushes

## Creating Scriptable Brushes

Create a new class inheriting from `GridBrushBase` (or any useful sub-classes of `GridBrushBase` like `GridBrush`). Override any required methods for your new `Brush` class. The following are the usual methods you would override:

* `Paint` allows the Brush to add items onto the target Grid
* `Erase` allows the Brush to remove items from the target Grid
* `FloodFill` allows the Brush to fill items onto the target Grid
* `Rotate` rotates the items set in the Brush.
* `Flip` flips the items set in the Brush.

Create instances of your new class using `ScriptableObject.CreateInstance<(Your Brush Class>()`. You may convert this new instance to an Asset in the Editor in order to use it repeatedly by calling `AssetDatabase.CreateAsset()`.

You can also make a custom editor for your brush. This works the same way as custom editors for scriptable objects. The following are the main methods you would want to override when creating a custom editor:

* You can override `OnPaintInspectorGUI` to have an inspector show up on the Palette when the Brush is selected to provide additional behaviour when painting.
* You can also override `OnPaintSceneGUI` to add additional behaviour when painting on the `SceneView`.
* You can also override `validTargets` to have a custom list of targets which the Brush can interact with. This list of targets is shown as a dropdown in the Palette window.

When created, the Scriptable Brush is listed in the __Brushes Dropdown__ in the Palette window. By default, an instance of the Scriptable Brush script is instantiated and stored in the _Library_ folder of your project. Any modifications to the brush properties are stored in that instance. If you want to have multiple copies of that Brush with different properties, you can instantiate the Brush as Assets in your project. These Brush Assets are listed separately in the Brush dropdown.

You can add a `CustomGridBrush` attribute to your Scriptable Brush class. This allows you to configure the behaviour of the Brush in the Palette window. The `CustomGridBrush` attribute has the following properties:

* `HideAssetInstances` - Setting this to true hides all copies of created Brush Assets in the Palette window. Set this if you only want the default instance to show up in the Brush dropdown in the Palette window.
* `HideDefaultInstances` - Setting this to true hides the default instance of the Brush in the Palette window. Set this if you only want created Assets to show up in the Brush dropdown in the Palette window.
* `DefaultBrush` - Setting this to true sets the default instance of the Brush as the default Brush in the project. This makes this Brush the default selected Brush whenever the project starts up. Only set one Scriptable Brush to be the Default Brush!
* `DefaultName` - Setting this makes the Brush dropdown use this as the name for the Brush instead of the name of the class of the Brush.

Remember to save your project to ensure that your new Brush Assets are saved!

---

* <span class="page-edit">2017-09-06 <!-- include IncludeTextNewPageSomeEdit --></span>