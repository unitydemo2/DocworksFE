# Views menu

The __Views__ menu is located in the top-left corner of the Look Dev view, next to the __Settings__ menu. This controls all the options specific to each individual view.

![__Views__ menu](../uploads/Main/LookDev-ViewsMenu.png)

|**Property** |**Function** |
|:---|:---|
| __Shading__ |	Select the drop-down menu to choose the shading mode. Shaded is the default. Unity-supported debug modes are also available here (for example, __Normal__ and __Albedo__).|
| __EV (Exposure Value)__ |Use the slider to define the Exposure Value on the HDRI buffer before tone mapping.|
| __Environment__ |	Use the slider to choose which environment the view should use from the list in the [HDRI view](LookDevHDRIView).|
| __Rotation__ |	Use the slider to rotate the environment around the GameObject. This rotation is added to the offset specific to each environment.|
| __LoD or LoD (auto)__ |	Available only if the Prefab supports LOD. Use this slider to control level of detail (LOD) for the GameObject. Set it to -1 for automatic LOD (auto) selection.|

If a multi-view mode is enabled, both views have their own settings. This is indicated by orange or blue to match the screen they represent.

![__Views__ menu in multi-view mode](../uploads/Main/LookDevControlMenus-MultiViewMode.png)