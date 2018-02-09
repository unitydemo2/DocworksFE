# HDRI menus

## HDRI main settings

Use these settings to apply lighting and shadow changes to all HDRIs in the [HDRI view](LookDevHDRIView) with one action.

![Main setting buttons](../uploads/Main/LookDevHDRIMenu-HDRIMainSettings-3.png)

Use the lightbulb button to synchronise light placement vertically across all HDRI environments. This is useful if you are switching from one environment to another and you want to keep the shadow direction similar for comparison.

![The lighbulb button synchronises light placement ](../uploads/Main/LookDevHDRIMenu-LightbulbButton-5.png)


![](../uploads/Main/LookDevHDRIMenu-ResetButton-6.png): Use this button to reset the lighting position of all HDRIs.

##HDRI individual settings

![Click on the 3-lines button (highlighted here) to access each HDRI's properties menu](../uploads/Main/LookDevHDRIMenu-0.png)

Each HDRI has its own menu to control its properties. To access this, click on the three-lines button (a representation of three sliders) underneath the __Environment__ button.

### Environment

|**Menu Item**|	**Properties**|
|:---|:---|
| __Angle Offset__ | Give a number by which to offset the angle of the HDRI (shortcut: left click+Ctrl on the HDRI thumbnail in the HDRI View). This offset is unique to the HDRI selected and is different from the __Rotation__ slider in the Look Dev [Views menu](LookDevViewsMenus), which works independently from the HDRI offset.|
| __Reset Environment__ | Resets the Angle offset to default (0).|

![An environment in Look Dev with two different angle offsets applied to it](../uploads/Main/LookDevHDRIMenu-Environment-1.png)

### Shadows

This applies only if __Environment Shadow__ is enabled.

|**Menu item**|	**Properties**|
|:---|:---|
| __Shadow brightness__ |Controls the brightness of the shadow.|
| __Color__ |Controls the color of the shadow. This is useful to match particular lighting conditions (for example if the lighting is all blue).|
| __Set to brightest__ |Sets the position of the shadow direction to the brightest texel of the HDRI thumbnail.|
| __Reset Shadows__ |Resets all shadow controls to default.|

![The __Shadows__ menu](../uploads/Main/LookDevHDRIMenu-Shadows-2.png)

