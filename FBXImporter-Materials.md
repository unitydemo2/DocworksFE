# Model Importer: Materials

By default, Unity uses a diffuse Material on imported Assets. Use the FBX Importer's __Materials__ tab to import Materials from your imported Assets. 

When you first open the __Materials__ tab, it looks like this:

![](../uploads/Main/FBXImporter-Materials-0.png)

Tick __Import Materials__ to open the settings for importing Materials from your imported Assets. 

![](../uploads/Main/FBXImporter-Materials-1.png)

The settings in the __Materials__ tab differ depending on the __Location__ you choose. There are two __Location__ options:

| __Location__| __Properties__ |
|:---|:---| 
| __Use Embedded Materials__| Choose this option to extract imported Materials as external Assets. This is the default option from Unity 2017.2 onwards. |
| __Use External Materials (Legacy)__| Choose this option to keep the imported Materials inside the imported Asset. This is a Legacy way of handling Materials, and is intended for projects created with 2017.1 or previous versions of Unity. This is the default option for Unity 2017.1 and previous versions of Unity. |

The following sections describe the settings for each Location option. 

## Location: Use Embedded Materials

![](../uploads/Main/FBXImporter-Materials-2.png)

| __Property__|| __Function__ |
|:---|:---|:---| 
| __Textures__|| Click the __Extract Textures__ button to extract Textures that are embedded in your imported Asset. This is greyed out if there are no Textures to extract. |
| __Materials__|| Click the __Extract Materials__ button to extract Materials that are embedded in your imported Asset. This is greyed out if there are no materials to extract. |
| __Remapped Materials__|||
| __On Demand Remap__|| These settings match the settings that appear in the inspector if you set the __Location__ to __Use External Materials (Legacy)__. See the table above for descriptions of these properties. |
|| __Naming__ | Use this to define how Unity Materials are named. |
|| By Base Texture Name | The name of the diffuse Texture of the imported Material that is used to name the Material in Unity. When a diffuse Texture is not assigned to the Material, Unity uses the name of the imported Material. |
|| From Model’s Material | The name of the imported Material is used for naming the Unity Material. |
|| Model Name + Model’s Material | The name of the model file in combination with the name of the imported Material is used for naming the Unity Material. |
|| __Search__ | Use this to define where Unity tries to locate existing Materials using the name defined by the __Naming__ option. |
|| Local | Unity tries to find existing Materials in the "local" Materials folder only (that is, the *Materials* subfolder, which is the same folder as the model file). |
|| Recursive-Up | Unity tries to find existing Materials in all Materials subfolders in all parent folders up to the Assets folder. |
|| Everywhere | Unity tries to find existing Materials in all Unity project folders. |
|| __Search and Remap__ | Use this button to remap your imported Materials to existing Material Assets, using the same settings as the Legacy import option. Clicking this button does not extract the Materials from the Asset, and does not change anything if Unity cannot find any materials with the correct name.  |
| __List of imported materials__|| This list displays all imported Materials found in the Asset. You can remap each material to an existing Material Asset in your Project. |



If you want to modify the properties of the Materials in Unity, you can extract them all at once using the __Extract Materials__ button. If you want to extract them one by one, go to __Assets__ &gt; __Extract From Prefab__. When you extract Materials this way, they appear as references in the __Remapped Materials__ list.

New imports or changes to the original Asset do not affect extracted Materials. If you want to re-import the Materials from the source Asset, you need to remove the references to the extracted Materials in the __Remapped Materials__ list. To remove an item from the list, select it and press the Backspace key on your keyboard.

## Location: Use External Materials (Legacy)

Choose this option to extract imported Materials as external Assets. Before Unity version 2017.2, this was the default way of handling Materials. When opening projects created with 2017.1 or previous versions of Unity, only the Legacy settings and the __Material Location__ option are visible.

![](../uploads/Main/FBXImporter-Materials-3.png)

| __Property__|| __Function__ |
|:---|:---|:---| 
| __Naming__|| Use this to define how Unity Materials are named. |
|| By Base Texture Name | The name of the diffuse Texture of the imported Material that is used to name the Material in Unity. When a diffuse Texture is not assigned to the Material, Unity uses the name of the imported Material. |
|| From Model’s Material | The name of the imported Material is used for naming the Unity Material. |
|| Model Name + Model’s Material | The name of the model file in combination with the name of the imported Material is used for naming the Unity Material. |
| __Search__|| Use this to define where Unity tries to locate existing Materials using the name defined by the __Naming__ option. |
|| Local | Unity tries to find existing Materials in the "local" Materials folder only (that is, the *Materials* subfolder, which is the same folder as the model file). |
|| Recursive-Up | Unity tries to find existing Materials in all Materials subfolders in all parent folders up to the Assets folder. |
|| Everywhere | Unity tries to find existing Materials in all Unity project folders. |



