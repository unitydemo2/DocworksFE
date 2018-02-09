Custom Editors
==============

A key to increasing the speed of game creation is to create custom editors for commonly used components. For the sake of example, we'll use this very simple script that always keeps an object looking at a point. Add this script to your project, and place it onto a cube gameobject in your scene. The script should be named "LookAtPoint"

````
//C# Example (LookAtPoint.cs)
using UnityEngine;
public class LookAtPoint : MonoBehaviour
{
    public Vector3 lookAtPoint = Vector3.zero;

    void Update()
    {
        transform.LookAt(lookAtPoint);
    }
}
````

````
//JS Example (LookAtPoint.js)
#pragma strict
var lookAtPoint = Vector3.zero;
function Update()
{
    transform.LookAt(lookAtPoint);
}
````

This will keep an object oriented towards a world-space point. Currently this script will only become active in **play mode**, that is, when the game is running. When writing editor scripts it's often useful to have certain scripts execute during **edit mode** too, while the game is not running. You can do this by adding an ExecuteInEditMode attribute to it:

````
//C# Example (LookAtPoint.cs)
using UnityEngine;
[ExecuteInEditMode]
public class LookAtPoint : MonoBehaviour
{
    public Vector3 lookAtPoint = Vector3.zero;

    void Update()
    {
        transform.LookAt(lookAtPoint);
    }
}
````

````
//JS Example (LookAtPoint.js)
#pragma strict
@script ExecuteInEditMode()
var lookAtPoint = Vector3.zero;
function Update()
{
    transform.LookAt(lookAtPoint);
}
````

Now if you move the object which has this script around in the editor, or change the values of "Look At Point" in the inspector - even when not in play mode - the object will update its orientation correspondingly so it remains looking at the target point in world space.

###Making a Custom Editor

The above demonstrates how you can get simple scripts running during edit-time, however this alone does not allow you to create your own editor tools. The next step is to create a __Custom Editor__ for script we just created.

When you create a script in Unity, by default it inherits from MonoBehaviour, and therefore is a **Component** which can be placed on a game object. When placed on a game object, the Inspector displays a default interface for viewing and editing all public variables that can be shown - such as integers, floats, strings, Vector3's, etc.

Here's how the default inspector looks for our script above:

![A default inspector with a public Vector3 field](../uploads/Main/NoCustomInspector.png)

**A custom editor is a separate script which *replaces* this default layout with any editor controls that you choose.**

To begin creating the custom editor for our LookAtPoint script, you should create another script with the same name, but with "Editor" appended. So for our example: "LookAtPointEditor".

````
//c# Example (LookAtPointEditor.cs)
using UnityEngine;
using UnityEditor;
​
[CustomEditor(typeof(LookAtPoint))]
[CanEditMultipleObjects]
public class LookAtPointEditor : Editor 
{
    SerializedProperty lookAtPoint;
    
    void OnEnable()
    {
        lookAtPoint = serializedObject.FindProperty("lookAtPoint");
    }
​
    public override void OnInspectorGUI()
    {
        serializedObject.Update();
        EditorGUILayout.PropertyField(lookAtPoint);
        serializedObject.ApplyModifiedProperties();
    }
}
````

````
//JS Example (LookAtPointEditor.js)
#pragma strict
@CustomEditor(LookAtPoint)
@CanEditMultipleObjects
class LookAtPointEditor extends Editor {

    var lookAtPoint : SerializedProperty;

    function OnEnable()
    {
        lookAtPoint = serializedObject.FindProperty("lookAtPoint");
    }

    function OnInspectorGUI()
    {
        serializedObject.Update();
        EditorGUILayout.PropertyField(lookAtPoint);
        serializedObject.ApplyModifiedProperties();
    }
}
````

This class has to derive from **Editor**. The **CustomEditor** attribute informs Unity which component it should act as an editor for. The **CanEditMultipleObjects** attribute tells Unity that you can select multiple objects with this editor and change them all at the same time.

The code in OnInspectorGUI is executed whenever Unity displays the editor in the Inspector. You can put any GUI code in here - it works just like OnGUI does for games, but is run inside the Inspector. Editor defines the target property that you can use to access the object being inspected. Here's what our custom inspector looks like:

![](../uploads/Main/CustomInspector.png) 

It's not very interesting because all we have done so far is to recreate the Vector3 field, exactly like the default inspector shows us, so the result looks very similar (although the "Script" field is now not present, because we didn't add any inspector code to show it).

However now that you have control over how the inspector is displayed in an Editor script, you can use any code you like to lay out the inspector fields, allow the user to adjust the values, and even display graphics or other visual elements. In fact all of the inspectors you see within the Unity Editor including the more complex inspectors such as the terrain system and animation import settings, are all made using the same API that you have access to when creating your own custom Editors.

Here's a simple example which extends your editor script to display a message indicating whether the target point is above or below the gameobject:


````
//c# Example (LookAtPointEditor.cs)
using UnityEngine;
using UnityEditor;

[CustomEditor(typeof(LookAtPoint))]
[CanEditMultipleObjects]
public class LookAtPointEditor : Editor
{
    SerializedProperty lookAtPoint;

    void OnEnable()
    {
        lookAtPoint = serializedObject.FindProperty("lookAtPoint");
    }

    public override void OnInspectorGUI()
    {
        serializedObject.Update();
        EditorGUILayout.PropertyField(lookAtPoint);
        serializedObject.ApplyModifiedProperties();
        if (lookAtPoint.vector3Value.y > (target as LookAtPoint).transform.position.y)
        {
            EditorGUILayout.LabelField("(Above this object)");
        }
        if (lookAtPoint.vector3Value.y < (target as LookAtPoint).transform.position.y)
        {
            EditorGUILayout.LabelField("(Below this object)");
        }
    }
}
````

````
//JS Example (LookAtPointEditor.js)
#pragma strict
@CustomEditor(LookAtPoint)
@CanEditMultipleObjects
class LookAtPointEditor extends Editor {

    var lookAtPoint : SerializedProperty;

    function OnEnable()
    {
        lookAtPoint = serializedObject.FindProperty("lookAtPoint");
    }

    function OnInspectorGUI()
    {
        serializedObject.Update();
        EditorGUILayout.PropertyField(lookAtPoint);
        serializedObject.ApplyModifiedProperties();
        if (lookAtPoint.vector3Value.y > (target as LookAtPoint).transform.position.y)
        {
            EditorGUILayout.LabelField("(Above this object)");
        }
        if (lookAtPoint.vector3Value.y < (target as LookAtPoint).transform.position.y)
        {
            EditorGUILayout.LabelField("(Below this object)");
        }
    }
}
````

So now we have an new element to our inspector which prints a message showing if the target point is above or below the gameobject.

![](../uploads/Main/CustomInspector2.png) 

This is just scratching the surface of what you can do with Editor scripting. You have full access to all the IMGUI commands to draw any type of interface, including rendering scenes using a camera within editor windows.
 

###Scene View Additions
You can add extra code to the Scene View by implementing an OnSceneGUI in your custom editor. 

OnSceneGUI works just like OnInspectorGUI - except it gets run in the scene view. To help you make your own editing controls in the scene view, you can use the functions defined in [Handles](ScriptRef:Handles.html) class. All functions in there are designed for working in 3D Scene views.

````
//C# Example (LookAtPointEditor.cs)
using UnityEngine;
using UnityEditor;

[CustomEditor(typeof(LookAtPoint))]
[CanEditMultipleObjects]
public class LookAtPointEditor : Editor
{
    SerializedProperty lookAtPoint;

    void OnEnable()
    {
        lookAtPoint = serializedObject.FindProperty("lookAtPoint");
    }

    public override void OnInspectorGUI()
    {
        serializedObject.Update();
        EditorGUILayout.PropertyField(lookAtPoint);
        if (lookAtPoint.vector3Value.y > (target as LookAtPoint).transform.position.y)
        {
            EditorGUILayout.LabelField("(Above this object)");
        }
        if (lookAtPoint.vector3Value.y < (target as LookAtPoint).transform.position.y)
        {
            EditorGUILayout.LabelField("(Below this object)");
        }
        
            
        serializedObject.ApplyModifiedProperties();
    }

    public void OnSceneGUI()
    {
        var t = (target as LookAtPoint);

        EditorGUI.BeginChangeCheck();
        Vector3 pos = Handles.PositionHandle(t.lookAtPoint, Quaternion.identity);
        if (EditorGUI.EndChangeCheck())
        {
            Undo.RecordObject(target, "Move point");
            t.lookAtPoint = pos;
            t.Update();
        }
    }
}
````


````
//JS Example (LookAtPointEditor.js)
#pragma strict
@CustomEditor(LookAtPointJS)
@CanEditMultipleObjects
class LookAtPointEditorJS extends Editor {

    var lookAtPoint : SerializedProperty;

    function OnEnable()
    {
        lookAtPoint = serializedObject.FindProperty("lookAtPoint");
    }

    function OnInspectorGUI()
    {
        serializedObject.Update();
        EditorGUILayout.PropertyField(lookAtPoint);
        serializedObject.ApplyModifiedProperties();
        if (lookAtPoint.vector3Value.y > (target as LookAtPointJS).transform.position.y)
        {
            EditorGUILayout.LabelField("(Above this object)");
        }
        if (lookAtPoint.vector3Value.y < (target as LookAtPointJS).transform.position.y)
        {
            EditorGUILayout.LabelField("(Below this object)");
        }
    }


    function OnSceneGUI()
    {
        var t : LookAtPointJS = (target as LookAtPointJS);

        EditorGUI.BeginChangeCheck();
        var pos = Handles.PositionHandle(t.lookAtPoint, Quaternion.identity);
        if (EditorGUI.EndChangeCheck())
        {
            Undo.RecordObject(target, "Move point");
            t.lookAtPoint = pos;
            t.Update();
        }
    }
}

````

If you want to put 2D GUI objects (GUI, EditorGUI and friends), you need to wrap them in calls to Handles.BeginGUI() and Handles.EndGUI().
