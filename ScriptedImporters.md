## Scripted Importers

Scripted Importers are part of the [Unity Scripting API](ScriptingSection). Use Scripted Importers to write custom Asset importers in C# for file formats not natively supported by Unity.

Create a custom importer by specializing the abstract class [ScriptedImporter](ScriptRef:Experimental.AssetImporters.ScriptedImporter.html) and applying the [ScriptedImporter](ScriptRef:Experimental.AssetImporters.ScriptedImporterAttribute.html) attribute. This registers your custom importer to handle one or more file extensions. When a file matching the registered file extensions is detected by the Asset pipeline as being new or changed, Unity invokes the method `OnImportAsset` of your custom importer.

Note: Scripted Importers cannot handle a file extension that is already natively handled by Unity.

**Note: Limitation**

This is an experimental release of the Scripted Importer feature and as such is limited to assets that can be created using the Unity Scripting API. This is not a limitation of the implementation or design of the this feature, but does impose limits on its real-world use.


### Example

Below is a simple example as Scripted Importer: It imports asset files with the extension "cube" into a Unity Prefab with a cube primitive as the main Asset and a default material with a color fetched from the Asset file:

```
using System.IO;
using System.Text;
using UnityEditor.Experimental.AssetImporters;
using UnityEngine;

[ScriptedImporter(1, "cube")]
public class CubeImporter : ScriptedImporter
{
    [SerializeField]
    float m_ColorShift = 0f;

    public override void OnImportAsset(AssetImportContext ctx)
    {
        // Main asset
        var cube = GameObject.CreatePrimitive(PrimitiveType.Cube);
        ctx.SetMainAsset("MainAsset", cube);

        // Material as sub-asset
        string text = File.ReadAllText(ctx.assetPath, Encoding.UTF8);
        var channels = text.Split(',');
        var color = new Color(float.Parse(channels[0]) + m_ColorShift,
                              float.Parse(channels[1]) + m_ColorShift,
                              float.Parse(channels[2]) + m_ColorShift);

        var material = new Material(Shader.Find("Standard")) { color = color };
        cube.GetComponent<Renderer>().material = material;
        ctx.AddSubAsset("Material", material);
    }
}
```

**Note**: 

* The importer is registered with Unity's Asset pipeline by placing the the `ScriptedImporter` attribute on the CubeImporter class.
* The CubeImporter class implements the abstract `ScriptedImporter` base class.
* `OnImportAsset`’s ctx argument contains both input and output data for the import event.
* Each import event must generate one (and only one) call to `SetMainAsset`.
* Each import event may generate as many calls to `AddSubAsset` as necessary.
* Please refer to the [Scripting API documentation](ScrptRef:Experimental.AssetImporters.ScriptedImporter.html) for more details.

You may also implement a custom Import Settings Editor by specializing [ScriptedImporterEditor](ScriptRef:Experimental.AssetImporters.ScriptedImporterEditor) class and decorating it with the class attribute `CustomEditor` to tell it what type of importer it is used for.

For example:


```
using UnityEditor;
using UnityEditor.Experimental.AssetImporters;
using UnityEditor.SceneManagement;
using UnityEngine;

[CustomEditor(typeof(CubeImporter))]
public class CubeImporterEditor: ScriptedImporterEditor
{
    public override void OnInspectorGUI()
    {
        var colorShift = new GUIContent("Color Shift");
        var prop = serializedObject.FindProperty("m_ColorShift");
        EditorGUILayout.PropertyField(prop, colorShift);
        base.ApplyRevertGUI();
    }
}
```

### Using a Scripted Importer

Once you have added a scripted importer class to a project, you may use it just like any other native file type supported by Unity:

* Drop a supported file in the Asset directory hierarchy to import.
* Restarting the Unity Editor reimports any files that have changed since last update.
* Editing the Asset file on disk and returning to the Unity Editor triggers a reimport.
* Import a new asset using __Asset__ > __Import New Asset...__.
* Explicitly trigger a re-import via the menu: __Asset__ > __Reimport__.
* Click on the Asset to see its settings in the [Inspector window](UsingTheInspector). To modify its settings, edit them in the Inspector window and click __Apply__ .
<br/><br/>


![The Inspector window of an Asset (An Alembic Girl) imported by the Scripted Importer](../uploads/Main/ScriptedImporters-2.png)


### Real-world use of Scripted Importers

* __Alembic__: The Alembic importer plug-in has been updated to use a Scripted Importer. For more information, visit [Unity github: AlembicImporter](https://github.com/unity3d-jp/AlembicImporter).

* __USD__: The USD importer plug-in has been updated to use a Scripted Importer.
For more information, please visit [Unity github:: USDForUnity](https://github.com/unity3d-jp/USDForUnity).

<br/>
<br/>

---

* <span class="page-history">New feature in [2017.1](https://docs.unity3d.com/2017.1/Documentation/Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>

* <span class="page-edit">2017-07-27  <!-- include IncludeTextAmendPageNoEdit --></span>


