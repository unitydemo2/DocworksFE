# Sprite Atlas

Sprite Atlas is an asset

Sprite Atlas is created via the menu option in the Editor and will stay as an asset in the project’s folder (*.spriteatlas).

###Unified Settings

Sprite Atlas asset provides a set of texture settings for the packed texture. Regardless what was the texture settings of the sprite being pack in an atlas, the result atlas texture will only respect the settings in the atlas asset. 

###Runtime access

Sprite Atlas asset has a runtime representation which can be accessed during Runtime.

###Variants

User will be able to create another Sprite Atlas asset and declared it is a variant of one existing Sprite Atlas in the project. It then will duplicate the master’s atlas texture and resize it according to a multiplier.

The Sprite Packer is disabled by default but you can configure it from the Editor settings (__File Menu: Edit -> Project Settings -> Editor__). The sprite packing mode can be changed from Disabled to __Enabled for Builds__ where packing is used for builds only and not Play mode or __Always Enabled__ (Atlases will be packed before entering Play mode and for builds).

![](../uploads/Main/SpriteAtlas1.png)

## How to create a Sprite Atlas

The Sprite Atlas is a type of Asset in Unity projects. You can create them, and they are ready to use, via the Project View. To create a Sprite Atlas select __Asset -> Create -> Sprite Atlas__ from the main menu.

## Properties

![](../uploads/Main/SpriteAtlas2.png)

| Property| Function |
|:---|:---| 
| Type| Sets the type of atlas to be either a Master or Variant Atlas. |
| Include in build| Always includes the Atlas Asset in the build. |
| Allow Rotation| Allows sprites to be rotated for packing |
| Tight Packing| Non-rectangle packing |
| Read/Write Enabled| Set this to true if you want texture data to be readable from scripts. Set it to false to prevent scripts from reading texture data. |
| Generate Mip Maps| Select this to enable mip-map generation. Mip maps are smaller versions of the Texture that get used when the Texture is very small on screen. |
| Filter Mode| Select how the Texture is filtered |
| Platform-specific overrides panel| Use the Platform-specific overrides panel to set default options (using Default), and then override them for a specific platform using the buttons along the top of the panel.<br/>[https://docs.unity3d.com/Manual/class-TextureImporterOverride.html](class-TextureImporterOverride) |
| Objects For Packing| The objects to be included in the packed Atlas. Folders, Textures or individual sprites can be added to the list. |


### Assigning assets to be atlased

Folders, Textures or Sprites can be assigned to the Sprite Atlas. Entire folders can be assigned to the Sprite Atlas asset, all Textures within that folder including subfolders will be packed. When assigning an individual Texture, all defined sprites will be included. Single sprites can also be assigned to the atlas and other sprites within the same Texture will not be considered.

![](../uploads/Main/SpriteAtlas3.png)

1. To include assets to be atlased, select the Atlas asset and add them by either adding new entry to the list or dragging and dropping them from the Project onto the list area in the inspector. You can add the folders, textures, sprites to the atlas.

2. Set the desired settings for the generated atlas. Changes to the setting will always mark this atlas as modified and will be packed again during the packing phase.

3. The packed atlas can be previewed by pressing the "Pack Preview" button in the inspector. This will trigger a packing for this atlas. Once the packing is done, the texture will appear in the preview section.

4. All atlases with modified settings will be packed before entering Play Mode (if __Always Enabled__ is selected).

### Down-scaled variant (HD/SD)

User will be able to create another Sprite Atlas asset and declare it is a variant of an existing Sprite Atlas in the project. It will then duplicate the Master’s atlas texture and resize it according to a multiplier.

### Creating a Sprite Atlas variant

![](../uploads/Main/SpriteAtlas4.png)

1. Set the Type for the Sprite Atlas to Variant.
![](../uploads/Main/SpriteAtlas5.png)
2. Assign an atlas to the Master Atlas slot.
![](../uploads/Main/SpriteAtlas6.png)
3. Set the scaling factor for the variant. Value can be from 0.1 to 1.

4. To bind the variant atlas as default instead of the master, just check the "Include in build" option in the variant and uncheck the option in master.

5. Checking both will randomly include one of the atlas (master/variant). You might want to uncheck both to have late binding, mentioned below.

### Runtime sprites enumeration

1. Create a custom component that takes a "SpriteAtlas" as a variable.

2. Assign any of your existing Sprite Atlas to the field.

3. Enter play mode or run the player.

4. Access the variable and notice you can now call the property ".GetSprites" to get the array of Sprites packed in this atlas.

### Late Binding

A Sprite can be started in runtime as "packed but not referencing any atlas" and will appear blank until an atlas is bound to it. The benefit of this behaviour is to allow user to have chance to do late binding if the source of the atlas is not available during startup e.g. asset bundles downloaded from the web.

### Late Binding via callback

1. As long as the Sprite is packed into any Sprite Atlas but the sprite atlas is not bound as default (e.g. unchecked "Include in build" option) the Sprite will be invisible in the scene.

2. User can listen to callback SpriteAtlas.atlasRequested.

3. This delegate method will provide a tag of atlas which suppose to bind and a System.Action which takes in a SpriteAtlas asset. User is expected to load the asset by any mean (script references, Resources.load, Asset bundle) and supply the asset to the System.Action.

<br/>
----

* <span class="page-edit">2017-05-26 <!-- include IncludeTextNewPageNoEdit --></span>
 
* <span class="page-history">New in Unity [2017.1](../Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>


