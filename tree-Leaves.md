Leaf Group Properties
=====================


Leaf groups generate leaf geometry. Either from primitives or from user created meshes.

Distribution
------------

Adjusts the count and placement of leaves in the group. Use the curves to fine tune position, rotation and scale. The curves are relative to the parent branch.


![](../uploads/Main/TreeNode-LeafNodePropertiesDistribution.png) 


| | |
|:---|:---|
|__Group Seed__ |The seed for this group of leaves. Modify to vary procedural generation.|
|__Frequency__ |Adjusts the number of leaves created for each parent branch.|
|__Distribution__|Select the way the leaves are distributed along their parent.|
|__Twirl__ |Twirl around the parent branch.|
|__Whorled Step__|Defines how many nodes are in each whorled step when using Whorled distribution. For real plants this is normally a Fibonacci number.|
|__Growth Scale__|Defines the scale of nodes along the parent node. Use the curve to adjust and the slider to fade the effect in and out.|
|__Growth Angle__|Defines the initial angle of growth relative to the parent. Use the curve to adjust and the slider to fade the effect in and out.|

Geometry
--------

Select what type of geometry is generated for this leaf group and which materials are applied. If you use a custom mesh, its materials will be used.


![](../uploads/Main/TreeNode-LeafNodePropertiesGeometry.png) 


| | |
|:---|:---|
|__Geometry Mode__|The type of geometry created. You can use a custom mesh, by selecting the Mesh option, ideal for flowers, fruits, etc.|
|__Material__ |Material used for the leaves.|
|__Mesh__ |Mesh used for the leaves.|

Shape
-----

Adjusts the shape and growth of the leaves.


![](../uploads/Main/TreeNode-LeafNodePropertiesShape.png) 


| | |
|:---|:---|
|__Size__ |Adjusts the size of the leaves, use the range to adjust the minimum and the maximum size.|
|__Perpendicular Align__|Adjusts whether the leaves are aligned perpendicular to the parent branch.|
|__Horizontal Align__ |Adjusts whether the leaves are aligned horizontally.|

Animation
---------

Adjusts the parameters used for animating this group of leaves. Wind zones are only active in Play Mode. If you select too high values for Main Wind and Main Turbulence the leaves may float away from the branches.


![](../uploads/Main/TreeNode-LeafNodePropertiesAnimation.png) 


| | |
|:---|:---|
|__Main Wind__ |Primary wind effect. Usually this should be kept as a low value to avoid leaves floating away from the parent branch.|
|__Main Turbulence__|Secondary turbulence effect. For leaves this should usually be kept as a low value.|
|__Edge Turbulence__|Defines how much wind turbulence occurs along the edges of the leaves.|
