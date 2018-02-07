Branch Group Properties
=======================


Branch groups node is responsible for generating branches and fronds. Its properties appear when you have selected a branch, frond or branch + frond node.

Distribution
------------

Adjusts the count and placement of branches in the group. Use the curves to fine tune position, rotation and scale. The curves are relative to the parent branch or to the area spread in case of a trunk.


![](../uploads/Main/TreeNode-BranchPropertiesDistribution.png) 


| | |
|:---|:---|
|__Group Seed__ |The seed for this group of branches. Modify to vary procedural generation.|
|__Frequency__ |Adjusts the number of branches created for each parent branch.|
|__Distribution__|The way the branches are distributed along their parent.|
|__Twirl__ |Twirl around the parent branch.|
|__Whorled Step__|Defines how many nodes are in each whorled step when using Whorled distribution. For real plants this is normally a Fibonacci number.|
|__Growth Scale__|Defines the scale of nodes along the parent node. Use the curve to adjust and the slider to fade the effect in and out.|
|__Growth Angle__|Defines the initial angle of growth relative to the parent. Use the curve to adjust and the slider to fade the effect in and out.|


Geometry
--------

Select what type of geometry is generated for this branch group and which materials are applied. __LOD Multiplier__ allows you to adjust the quality of this group relative to tree's __LOD Quality__.


![](../uploads/Main/TreeNode-BranchPropertiesGeometry.png) 


| | |
|:---|:---|
|__LOD Multiplier__ |Adjusts the quality of this group relative to tree's LOD Quality, so that it is of either higher or lower quality than the rest of the tree.|
|__Geometry Mode__ |Type of geometry for this branch group: Branch Only, Branch + Fronds, Fronds Only.|
|__Branch Material__|The primary material for the branches.|
|__Break Material__ |Material for capping broken branches.|
|__Frond Material__ |Material for the fronds.|


Shape
-----

Adjusts the shape and growth of the branches. Use the curves to fine tune the shape, all curves are relative to the branch itself.


![](../uploads/Main/TreeNode-BranchPropertiesShape.png) 


| | |
|:---|:---|
|__Length__ |Adjusts the length of the branches.|
|__Relative Length__ |Determines whether the radius of a branch is affected by its length.|
|__Radius__ |Adjusts the radius of the branches, use the curve to fine-tune the radius along the length of the branches.|
|__Cap Smoothing__ |Defines the roundness of the cap/tip of the branches. Useful for cacti.|
|**Growth** |Adjusts the growth of the branches.|
|__Crinkliness__ |Adjusts how crinkly/crooked the branches are, use the curve to fine-tune.|
|__Seek Sun__ |Use the curve to adjust how the branches are bent upwards/downwards and the slider to change the scale.|
|**Surface Noise** |Adjusts the surface noise of the branches.|
|__Noise__ |Overall noise factor, use the curve to fine-tune.|
|__Noise Scale U__ |Scale of the noise around the branch, lower values will give a more wobbly look, while higher values gives a more stochastic look.|
|__Noise Scale V__ |Scale of the noise along the branch, lower values will give a more wobbly look, while higher values gives a more stochastic look.|
|**Flare** |Defines a flare for the trunk.|
|__Flare Radius__ |The radius of the flares, this is added to the main radius, so a zero value means no flares.|
|__Flare Height__ |Defines how far up the trunk the flares start.|
|__Flare Noise__ |Defines the noise of the flares, lower values will give a more wobbly look, while higher values gives a more stochastic look.|
|**Breaking** |Controls the breaking of branches.|
|__Break Chance__ |Chance of a branch breaking, i.e. 0 = no branches are broken, 0.5 = half of the branches are broken, 1.0 = all the branches are broken.|
|__Break Location__|This range defines where the branches will be broken. Relative to the length of the branch.|


![](../uploads/Main/TreeNode-BranchPropertiesShapeFrond.png) 

**These properties are for child branches only, not trunks.**

| **Welding ** | **Defines the welding of branches onto their parent branch. Only valid for secondary branches.** |
|:---|:---|
|__Weld Length__ |Defines how far up the branch the weld spread starts.|
|__Spread Top__ |Weld's spread factor on the top-side of the branch, relative to it's parent branch. Zero means no spread.|
|__Spread Bottom__ |Weld's spread factor on the bottom-side of the branch, relative to it's parent branch. Zero means no spread.|


Fronds
------

Here you can adjust the number of fronds and their properties. This tab is only available if you have Frond geometry enabled in the __Geometry__ tab.


![](../uploads/Main/TreeNode-BranchPropertiesFronds.png) 


| | |
|:---|:---|
|__Frond Count__ |Defines the number of fronds per branch. Fronds are always evenly spaced around the branch.|
|__Frond Width__ |The width of the fronds, use the curve to adjust the specific shape along the length of the branch.|
|__Frond Range__ |Defines the starting and ending point of the fronds.|
|__Frond Rotation__|Defines rotation around the parent branch.|
|__Frond Crease__ |Adjust to crease / fold the fronds.|


Wind
----

Adjusts the parameters used for animating this group of branches. The wind zones are only active in Play Mode.


![](../uploads/Main/TreeNode-BranchPropertiesAnimation.png) 


| | |
|:---|:---|
|__Main Wind__ |Primary wind effect. This creates a soft swaying motion and is typically the only parameter needed for primary branches.|
|__Edge Turbulence__ |Turbulence along the edge of fronds. Useful for ferns, palms, etc.|
|__Create Wind Zone__|Creates a [Wind Zone](class-WindZone).|
