#Managed Plugins

Usually, scripts are kept in a project as source files and compiled by Unity whenever the source changes. However, it is also possible to compile a script to a **dynamically linked library** (DLL) using an external compiler. The resulting DLL can then be added to the project and the classes it contains can be attached to objects just like normal scripts.

It is generally much easier to work with scripts than DLLs in Unity. However, you may have access to third party Mono code which is supplied in the form of a DLL. When developing your own code, you may be able to use compilers not supported by Unity (F#, for example) by compiling the code to a DLL and adding it to your Unity project. Also, you may want to supply Unity code without the source (for an Asset Store product, say) and a DLL is an easy way to do this.


##Creating a DLL

To create a DLL, you will first need a suitable compiler. Not all compilers that produce .NET code are guaranteed to work with Unity, so it may be wise to test the compiler with some available code before doing significant work with it. If the DLL contains no code that depends on the Unity API then you can simply compile it to a DLL using the appropriate compiler options. If you do want to use the Unity API then you will need to make Unity's own DLLs available to the compiler. On a Mac, these are contained in the application bundle (you can see the internal structure of the bundle by using the Show Package Contents command from the contextual menu; right click or ctrl-click the Unity application):-

The path to the Unity DLLs will typically be

	/Applications/Unity/Unity.app/Contents/Frameworks/Managed/

...and the two DLLs are called UnityEngine.dll and UnityEditor.dll.

On Windows, the DLLs can be found in the folders that accompany the Unity application. The path will typically be

	C:\Program Files\Unity\Editor\Data\Managed

...while the names of the DLLs are the same as for Mac OS.

The exact options for compiling the DLL will vary depending on the compiler used. As an example, the command line for the Mono C# compiler, **mcs**, might look like this on Mac OS:-

	mcs -r:/Applications/Unity/Unity.app/Contents/Frameworks/Managed/UnityEngine.dll -target:library ClassesForDLL.cs 

Here, the _-r_ option specifies a path to a library to be included in the build, in this case the UnityEngine library. The _-target_ option specifies which type of build is required; the word "library" is used to select a DLL build. Finally, the name of the source file to compile is _ClassesForDLL.cs_ (it is assumed that this file is in the current working folder, but you could specify the file using a full path if necessary). Assuming all goes well, the resulting DLL file will appear shortly in the same folder as the source file.


##Using the DLL

Once compiled, the DLL file can simply be dragged into the Unity project like any other asset. The DLL asset has a foldout triangle which can be used to reveal the separate classes inside the library. Classes that derive from MonoBehaviour can be dragged onto Game Objects like ordinary scripts. Non-MonoBehaviour classes can be used directly from other scripts in the usual way.


![A folded-out DLL with the classes visible](../uploads/Main/DLLScreenshot.png) 


##Step by Step Guide for MonoDevelop and Visual Studio

This section explains how to build and integrate a simple DLL example with MonoDevelop and Visual Studio and also how to prepare a debugging session for the DLL.


###Setting Up the Project

First, open MonoDevelop or Visual Studio and create a new project. In MonoDevelop, you do this by selecting __File &gt; New &gt; Solution__ and then choosing __C# &gt; Library__. In Visual Studio, you should select __File &gt; New &gt; Project__ and then choose __Visual C# &gt; Class Library__.

You then need to fill out the information for the new library:

* **Name** is the namespace (for this example use "DLLTest" as the name).
* **Location** is the parent folder of the project.
* **Solution name** is the folder of the project.

Next, you should add references to the Unity DLLs. In MonoDevelop, you should open the contextual menu For _References_ in the Solution Browser and choose __Edit References__. Then, choose the option __.Net Assembly tab &gt; File System &gt; select file__. In Visual Studio, open the contextual menu For _References_ in the Solution Explorer and choose __Add Reference__. Then, choose the option __Browse &gt; Browse &gt; select file__.

At this stage, you will have the option to select the required DLL file. On Mac OSX, the file can be found at

        Applications/Unity.app/Contents/Frameworks/Managed/UnityEngine.dll

...while on Windows, the path is

        Program Files\Unity\Editor\Data\Managed\UnityEngine.dll


###Code

For this example, rename the class to "MyUtilities" in the Solution browser and replace its code with the following:


````
using System;	
using UnityEngine;

namespace DLLTest {

	public class MyUtilities {
	
	    public int c;

	    public void AddValues(int a, int b) {
		    c = a + b;	
	    }
	
	    public static int GenerateRandom(int min, int max) {
	    	System.Random rand = new System.Random();
		    return rand.Next(min, max);
    	}
	}
}
````

With the code in place, build the project to generate the DLL file along with its debug symbols.


###Using the DLL in Unity

For this example, create a new project in Unity and copy the built file `<project folder>/bin/Debug/DLLTest.dll` into the Assets folder. Then, create a C# script called "Test" in Assets, and replace its contents with the following code:


````
using UnityEngine;
using System.Collections;
using DLLTest;

public class Test : MonoBehaviour {

	 void Start () {
		MyUtilities utils = new MyUtilities();
		utils.AddValues(2, 3);
		print("2 + 3 = " + utils.c);
	 }
	
	 void Update () {
		print(MyUtilities.GenerateRandom(0, 100));
	 }
}
````

When you attach this script to an object in the scene and press Play, you will see the output of the code from the DLL in the Console window.

###Setting Up a Debugging Session for the DLL

Firstly, you should prepare the debug symbols for the DLL. In MonoDevelop, copy the built file `<project folder>/bin/Debug/DLLTest.dll.mdb` into the Assets/Plugins folder. In Visual Studio, execute

	Program Files\Unity\Editor\Data\Mono\lib\mono\2.0\pdb2mdb.exe

in the command prompt, passing `<project folder>\bin\Debug\DLLTest.pdb` as a parameter. Then, copy the converted file `<project folder>\bin\Debug\DLLTest.dll.mdb` into Assets/Plugins.

Next, open the "Test" script in MonoDevelop. Make sure the Unity debugger is enabled from the Tools menu (Windows) or MonoDevelop-Unity menu (MacOS). The option you need from this menu is __Add-in Manager &gt; Installed tab &gt; Unity &gt; select Mono Soft Debugger Support for Unity &gt; Enable__.

With this setup completed, you can debug code that uses the DLL in Unity in the usual way. See the [Scripting Tools](ScriptingTools) section for further information about debugging.
