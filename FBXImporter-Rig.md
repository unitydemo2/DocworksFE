# Model Importer: Rig

The __Rig__ tab allows you to assign or create an avatar definition to your imported skinned Model so that you can animate it. See documentation on [Asset Preparation and Import](AssetPreparationandImport) for more details.

By default, the __Rig__ tab looks like this:

![The __Rig__ tab with __Animation Type__ set to __None__](../uploads/Main/Rig-0.png)

There are three __Animation Type__ options:

* __Generic__
* __Humanoid__
* __Legacy__

## Animation Type: Generic

If you have a non humanoid character e.g. a quadruped, or any animatable entity that you wish to use with [Mecanim](AnimationOverview) choose Generic. After choosing you will then need to identify a bone in the drop down to use as the root node.

![The __Rig__ tab with __Animation Type__ set to __Generic__](../uploads/Main/Rig-1.png)

## Animation Type: Humanoid

If you have a humanoid character (ie, two legs, two arms and a head) then choose Humanoid and ‘Create from this model’. An Avatar will be created to best match the bone hierarchy - see [Avatar Creation and Setup](AvatarCreationandSetup) or you can pick an alternative avatar Definition that has already been set up.

![The __Rig__ tab with __Animation Type__ set to __Humanoid__](../uploads/Main/MecanimImporterRigTab.png)

|**_Property:_** ||**_Function:_** |
|:---|:---|:---|
|__Animation Type__ ||The type of animation.|
||__None__|No animation present|
||__Legacy__|Legacy animation system|
||__Generic__|Generic Mecanim animation|
||__Humanoid__|Humanoid Mecanim animation system|
|__Avatar Definition__||Where to get the Avatar definition|
||__Create from this model__|The Avatar should be based on this model|
||__Copy from other Avatar__|Point to an Avatar config set up on another model. |
|__Configure...__||Go to the [Avatar configuration](ConfiguringtheAvatar)|
|__Optimize Game Object__||When turned on, the game object transform hierarchy of the imported character will be removed and stored in the Avatar and Animator component. The SkinnedMeshRenderers of the character will then directly use the Mecanim internal skeleton. This option improves the performance of the animated characters. You should turn it on for the final product. In optimized mode skinned mesh matrix extraction is also multithreaded. |

## Animation Type: Legacy

Choose legacy if you wish to use the legacy animation system and import and use animations as with 3.x.

![The __Rig__ tab with __Animation Type__ set to __Legacy__](../uploads/Main/Rig-3.png)

---

* <span class="page-edit"> 2017-12-05  <!-- include IncludeTextAmendPageSomeEdit --></span>

* <span class="page-history">__Materials__ tab added in [2017.2](https://docs.unity3d.com/2017.2/Documentation/Manual/30_search.html?q=newin20172) <span class="search-words">NewIn20172</span></span>