# What is a Null Reference Exception?

A `NullReferenceException` happens when you try to access a reference variable that isn't referencing any object.  If a reference variable isn't referencing an object, then it'll be treated as `null`.  The run-time will tell you that you are trying to access an object, when the variable is `null` by issuing a `NullReferenceException`.

Reference variables in c# and JavaScript are similar in concept to pointers in C and C++.  Reference types default to `null` to indicate that they are not referencing any object. Hence, if you try and access the object that is being referenced and there isn't one, you will get a `NullReferenceException`.

When you get a `NullReferenceException` in your code it means that you have forgotten to set a variable before using it.  The error message will look something like:

    NullReferenceException: Object reference not set to an instance of an object
      at Example.Start () [0x0000b] in /Unity/projects/nre/Assets/Example.cs:10 

This error message says that a `NullReferenceException` happened on line 10 of the script file `Example.cs`.  Also, the message says that the exception happened inside the `Start()` function.  This makes the Null Reference Exception easy to find and fix.  In this example, the code is:

    //c# example
    using UnityEngine;
    using System.Collections;

    public class Example : MonoBehaviour {

    	// Use this for initialization
	    void Start () {
		    GameObject go = GameObject.Find("wibble");
    		Debug.Log(go.name);
    	}
	
    }

The code simply looks for a game object called "wibble".  In this example there is no game object with that name, so the `Find()` function returns `null`.  On the next line (line 9) we use the `go` variable and try and print out the name of the game object it references.  Because we are accessing a game object that doesn't exist the run-time gives us a `NullReferenceException`

Null Checks
-----------
Although it can be frustrating when this happens it just means the script needs to be more careful.  The solution in this simple example is to change the code like this:

    using UnityEngine;
    using System.Collections;

    public class Example : MonoBehaviour {

    	void Start () {
	    	GameObject go = GameObject.Find("wibble");
		    if (go) {
			    Debug.Log(go.name);
    		} else {
    			Debug.Log("No game object called wibble found");
    		}
    	}
    	
    }

Now, before we try and do anything with the `go` variable, we check to see that it is not `null`.  If it it `null`, then we display a message.

Try/Catch Blocks
----------------
Another cause for `NullReferenceException` is to use a variable that should be initialised in the Inspector.  If you forget to do this, then the variable will be `null`.  A different way to deal with `NullReferenceException` is to use try/catch block.  For example, this code:


    using UnityEngine;
    using System;
    using System.Collections;

    public class Example2 : MonoBehaviour {

    	public Light myLight; // set in the inspector
	
	    void Start () {
		    try {
			    myLight.color = Color.yellow;
    		}		
    		catch (NullReferenceException ex) {
	    		Debug.Log("myLight was not set in the inspector");
		    }
	    }
	
    }

In this code example, the variable called `myLight` is a `Light` which should be set in the Inspector window.  If this variable is not set, then it will default to `null`.  Attempting to change the color of the light in the `try` block causes a `NullReferenceException` which is picked up by the `catch` block.  The `catch` block displays a message which might be more helpful to artists and game designers, and reminds them to set the light in the inspector.

Summary
-------

* `NullReferenceException` happens when your script code tries to use a variable which isn't set (referencing) and object.
* The error message that appears tells you a great deal about where in the code the problem happens.
* `NullReferenceException` can be avoided by writing code that checks for `null` before accessing an object, or uses try/catch blocks.
