
Variables and the Inspector
=============================

When creating a script, you are essentially creating your own new type of component that can be attached to Game Objects just like any other component.

Just like other Components often have properties that are editable in the inspector, you can allow values in your script to be edited from the Inspector too.



````
using UnityEngine;
using System.Collections;

public class MainPlayer : MonoBehaviour {
	public string myName;
	
	// Use this for initialization
	void Start () {
		Debug.Log("I am alive and my name is " + myName);
	}
	
	// Update is called once per frame
	void Update () {
	
	}
}

````

This code creates an editable field in the Inspector labelled "My Name".


![](../uploads/Main/EditingVarInspector.png) 

Unity creates the Inspector label by introducing a space wherever a capital letter occurs in the variable name. However, this is purely for display purposes and you should always use the variable name within your code. If you edit the name and then press Play, you will see that the message includes the text you entered.


![](../uploads/Main/DebugLogMessage.png) 

In C#, you must declare a variable as public to see it in the Inspector. In UnityScript, variables are public by default unless you specify that they should be private:



````
#pragma strict

private var invisibleVar: int;

function Start () {

}

````

Unity will actually let you change the value of a script's variables while the game is running. This is very useful for seeing the effects of changes directly without having to stop and restart. When gameplay ends, the values of the variables will be reset to whatever they were before you pressed Play. This ensures that you are free to tweak your object's settings without fear of doing any permanent damage.
