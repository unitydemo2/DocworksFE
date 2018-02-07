Visual Studio C# integration
============================

Benefits of using Visual Studio
------------------------------

A more sophisticated C# development environment. 
Think smart autocompletion, computer-assisted changes to source files, smart syntax highlighting and more.

The difference between Community, Express and Pro
----------------------------------------------

VisualStudio C# is an Integrated Development Environment (IDE) tool from Microsoft.
Visual Studio now comes in three editions, [Community](https://www.visualstudio.com/vs/community/) (free to use) [Professional](http://www.microsoft.com/visualstudio/en-us/products/professional/default.mspx) (paid) and [Enterprise](https://www.visualstudio.com/vs/enterprise/) (paid). A comparison of feature differences between versions is available on the [Visual Studio website](https://www.visualstudio.com/vs/compare/).

Unity's Visual Studio integration allows you to create and maintain Visual Studio project files automatically. Also, VisualStudio will open when you double click on a script or on an error message in the Unity console.

Using Visual Studio with Unity
------------------------------------------------
Follow these steps to configure the Unity Editor to use Visual Studio as its default IDE:

In Unity, go to __Edit > Preferences__, and make sure that Visual Studio is selected as your preferred external editor.


![External Tool Settings](../uploads/Main/external_tools.png)

Next, doubleclick a C# file in your project. Visual Studio should automatically open that file for you.

You can edit the file, save, and switch back to Unity to test your changes.

A few things to watch out for
------------------------------

* Even though Visual Studio comes with its own C# compiler, and you can use it to check if you have errors in your c# scripts, Unity still uses its own C# compiler to compile your scripts. Using the Visual Studio compiler is still quite useful, because it means you don't have to switch to Unity all the time to check if you have any errors or not.


* Visual Studio's C# compiler has some more features than Unity's C# compiler currently supports. This means that some code (especially newer c# features) will not throw an error in Visual Studio but will in Unity.


* Unity automatically creates and maintains a Visual Studio .sln and .csproj file. Whenever somebody adds/renames/moves/deletes a file from within Unity, Unity regenerates the .sln and .csproj files. You can add files to your solution from Visual Studio as well. Unity will then import those new files, and the next time Unity creates the project files again, it will create them with this new file included.
