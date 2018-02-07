# Remote Settings component

Use the Remote Settings [component](Components) to control the properties of other components in your Scene without writing any code. The Remote Settings component is part of the Remote Settings plug-in, which you can download from the [Unity Asset Store](https://www.assetstore.unity3d.com/#!/content/89317).

Before using the Remote Settings component, you must [enable Remote Settings](UnityAnalyticsRemoteSettingsEnabling) in your project and should also [create your Remote Settings key-value pairs](UnityAnalyticsRemoteSettingsCreating) using the Unity Analytics Dashboard. 

You can place the Remote Settings component on the same GameObject as another component you want to control, or place it on a different GameObject. The only requirement is that both the Remote Settings component and any controlled components are active in the same Scene. 

## Using the Remote Settings component

To connect a remote setting to a component property or field:

1. Go to __Window__ > __Unity Analytics__ > __Remote Settings__ to open the Remote Settings window.

2. Choose the configuration (__Release__ or __Development__) that contains the setting you are going to connect.

3. Go to the Inspector window for the GameObject that you want to hold the Remote Settings component.

4. Click the __Add Component__ button.

5. Find the __Analytics__ > __RemoteSettings__ script in the list.

    ![](../uploads/Main/AnalyticsRemoteSettingsAddComponent.png)
    

6. Click __Add Component__ to add the Remote Settings component to the GameObject.

    ![](../uploads/Main/AnalyticsRemoteSettingsEmptyComponent.png)

7. To add a new parameter mapping, click the __+__ icon at the bottom of the Remote Setting component’s __Parameters__ list.

8. Drag the GameObject or the component that you want to remotely control to the parameter’s __Object__ field.

    ![](../uploads/Main/AnalyticsRemoteSettingsComponentEdit.png)

9. Select the property or field you want to control in the parameter’s __Field__ drop-down list.

10. Choose the __Remote Setting Key__ that you want to use to control this component property or field.

    ![](../uploads/Main/AnalyticsRemoteSettingsComponentComplete.png)

11. Click the __+__ icon to add additional parameters.

If no __Remote Settings Key__ names appear in the list, open the __Remote Settings__ window (menu: __Window__ > __Unity Analytics__ > __Remote Settings__) and click __Refresh__. If your remote settings still do not display in this window, check that you have an Internet connection and that your project is properly set up (see [Enabling Remote Settings](UnityAnalyticsRemoteSettingsEnabling)).

If the wrong keys appear in the list of key names, open the Remote Settings window (menu: __Window__ > __Unity Analytics__ > __Remote Settings__) and set the __Active Configuration__ to the configuration containing the correct set of keys.

The Remote Settings component cannot set the variables of [prefabs](Prefabs) that Unity loads later in the Scene than the component itself. Similarly, a Remote Settings component that is loaded later in the Scene can only set variables of objects that are part of the same prefab. Use more than one Remote Settings component to handle these types of situations. 

## Setting non-primitive properties

You can use the Remote Settings component to set the primitive fields and properties of an object directly. However, to set the variables of an object’s non-primitive members, you do have to write some additional code. The easiest approach is to add primitive-type properties to an object that you can set using the Remote Settings component. Then, implement the setter functions of these properties to update the intended variables of the non-primitive objects.   

**Code example**

In the example below, the class sets the base color of the Material assigned to a rendered GameObject. To do this, the class defines a primitive string-type property that takes an HTML-style color string. The setter for this property parses the string and sets the Material color accordingly. 

```
using UnityEngine;

public class RemoteColorChanger : MonoBehaviour
{
    private string _colorString = "";
    public string ColorString {

        get { 
            return _colorString; 
        }

        set { 
            Color colorObject;
            if (ColorUtility.TryParseHtmlString (value, out colorObject)) {
                _colorString = value;
                Renderer renderer = GetComponent<Renderer> ();

                if (renderer != null) {
                    MaterialPropertyBlock materialProperties = new MaterialPropertyBlock ();
                    renderer.GetPropertyBlock (materialProperties);
                    materialProperties.SetColor ("_Color", colorObject);
                    renderer.SetPropertyBlock (materialProperties);
                } 
            } else {
                Debug.LogWarning ("Invalid color string: " + value);
            }
        }
    }
}
```

**Using the code example**

You can add this `RemoteColorChanger` script to any `GameObject` that has a `Renderer` component. You can then use the Remote Settings component to map a setting key to the `ColorString` property. In this example, the script is a component of a `Cube` object.

![A Remote Settings component mapping the `ColorString` Remote Setting key](../uploads/Main/AnalyticsRemoteSettingsComponentComplete.png)

The matching key-value pair on the Remote Settings page of your Analytics Dashboard looks like the following:

![The `ColorString` setting defined on the Analytics Dashboard](../uploads/Main/AnalyticsSingleSetting.png)

Use the same technique to set any non-primitive value.  

<br/>
<br/>
---

* <span class="page-edit">2017-05-30 <!-- include IncludeTextNewPageYesEdit --></span>

* <span class="page-edit">2017-05-30 - Service compatible with Unity 5.5 onwards at this date but version compatibility may be subject to change.</span>
 
* <span class="page-history">New feature in Unity 2017.1</span>
