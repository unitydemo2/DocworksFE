#Searching

When working with large complex scenes it can be useful to search for specific objects. By using the __Search__ feature in Unity, you can filter out only the object or group of objects that you want to see. You can search assets by their name, by Component type, and in some cases by asset _Labels_ (see below). You can specify the search mode by choosing from the Search drop-down menu.


##Scene Search

Both the Scene and Hierarchy views have a search box that allows you to filter objects by their names. Since the two views are basically just different representations of the same set of objects, any search query you type will be duplicated in both search boxes and applied to both views at the same time. Note that both views change slightly when a search is active: the Scene View will show filtered-out objects in grey and the Hierarchy view will lose the hierarchic information and simply show objects listed by name:

![Scene and Hierarchy views with search filtering applied.](../uploads/Main/SceneSearchName35.png) 

The small cross button at the right of the search box removes the search query and restores the view to normal. The menu at the left hand side of the box lets you choose whether to filter objects by name, by type or both at once.



##Project Search and Labels

There is also a search box in the Project view. The search applies to _assets_ rather than their instances in the scene. 

One additional option available for assets is to search by __Labels__ as well as by name and type. A label is simply a short piece of text that you can use to group particular assets. If you click on the label button second from the left of the Project window  you will see a menu of existing labels with a text box at the top. You can then request assets assigned specific label.  Also you can create new labels.  For example you could add a "Vehicles" label to make all vehicle assets easy to locate. You can add a label to an asset from the _Asset Labels_ box at the bottom of its inspector. 

![Adding a "Prop" label](../uploads/Main/LabelBox.png)

The text box lets you filter the existing labels or enter the text of a new label; you can press the spacebar or enter key while typing to add the new label text to the asset. Labels currently applied to an asset are shown with a check mark to their left in the menu. You can simply "select" an applied label from the menu to remove it. Note that any asset can have as many labels as desired and thereby belong to several different label groups at once.

See [Inspector](UsingTheInspector) manual page for more informatation. 
