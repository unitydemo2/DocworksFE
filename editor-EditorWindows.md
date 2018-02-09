Editor Windows
==============


You can create any number of custom windows in your app. These behave just like the Inspector, Scene or any other built-in ones. This is a great way to add a user interface to a sub-system for your game.


![Custom Editor Interface by Serious Games Interactive used for scripting cutscene actions](../uploads/Main/CustomEditorWindow.png) 

Making a custom Editor Window involves the following simple steps:

* Create a script that derives from EditorWindow.
* Use code to trigger the window to display itself.
* Implement the GUI code for your tool.

###Derive From EditorWindow
In order to make your Editor Window, your script must be stored inside a folder called "Editor". Make a class in this script that derives from EditorWindow. Then write your GUI controls in the inner OnGUI function.



````
//JS Example

class MyWindow extends EditorWindow {
    function OnGUI () {
        // The actual window code goes here
    }
}


````
````
//C# Example

using UnityEngine;
using UnityEditor;
using System.Collections;

public class Example : EditorWindow

    {
	    void OnGUI () {
		    // The actual window code goes here
	       }
    }

````
_MyWindow.js - placed in a folder called 'Editor' within your project._

###Showing the window
In order to show the window on screen, make a menu item that displays it. This is done by creating a function which is activated by the 
__MenuItem__ property. 

The default behavior in Unity is to recycle windows (so selecting the menu item again would show existing windows. This is done by using the function [EditorWindow.GetWindow](ScriptRef:EditorWindow.GetWindow.html) Like this:


````
//JS Example

class MyWindow extends EditorWindow {
    @MenuItem ("Window/My Window")
    static function ShowWindow () {
        EditorWindow.GetWindow (MyWindow);
    }

    function OnGUI () {
        // The actual window code goes here
    }
}
````

````
//C# Example

using UnityEngine;
using UnityEditor;
using System.Collections;

class MyWindow : EditorWindow {
	[MenuItem ("Window/My Window")]

	public static void  ShowWindow () {
		EditorWindow.GetWindow(typeof(MyWindow));
	}
	
	void OnGUI () {
		// The actual window code goes here
	}
}
````

_Showing the MyWindow_

This will create a standard, dockable editor window that saves its position between invocations, can be used in custom layouts, etc. To have more control over what gets created, you can use [GetWindowWithRect](ScriptRef:EditorWindow.GetWindowWithRect.html)

###Implementing Your Window's GUI

The actual contents of the window are rendered by implementing the OnGUI function. You can use the same UnityGUI classes you use for your ingame GUI (__GUI__ and __GUILayout__). In addition we provide some additional GUI controls, located in the editor-only classes __EditorGUI__ and __EditorGUILayout__. These classes add to the controls already available in the normal classes, so you can mix and match at will.

The following C# code shows how you can add GUI elements to your custom EditorWindow:


````
//C# Example
using UnityEditor;
using UnityEngine;

public class MyWindow : EditorWindow
{
	string myString = "Hello World";
	bool groupEnabled;
	bool myBool = true;
	float myFloat = 1.23f;
	
	// Add menu item named "My Window" to the Window menu
	[MenuItem("Window/My Window")]
	public static void ShowWindow()
	{
		//Show existing window instance. If one doesn't exist, make one.
		EditorWindow.GetWindow(typeof(MyWindow));
	}
	
	void OnGUI()
	{
		GUILayout.Label ("Base Settings", EditorStyles.boldLabel);
		myString = EditorGUILayout.TextField ("Text Field", myString);
        
		groupEnabled = EditorGUILayout.BeginToggleGroup ("Optional Settings", groupEnabled);
			myBool = EditorGUILayout.Toggle ("Toggle", myBool);
			myFloat = EditorGUILayout.Slider ("Slider", myFloat, -3, 3);
		EditorGUILayout.EndToggleGroup ();
	}
}


````

This example results in a window which looks like this:

![Custom Editor Window created using supplied example.](../uploads/Main/ExampleEditorWindow.png) 


For more info, take a look at the example and documentation on the [EditorWindow page](ScriptRef:EditorWindow.html).
