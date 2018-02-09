#MonoDevelop

__MonoDevelop__ is the _integrated development environment_ (IDE) supplied with Unity. An IDE combines the familiar operation of a text editor with additional features for debugging and other project management tasks. The text editor will not be covered here since it is fairly intuitive, but the integration of the editor and debugger with Unity are described below.

##Setting Up MonoDevelop

MonoDevelop is installed by default with Unity, although there is the option to exclude it from the installation on Windows. You should check that MonoDevelop is set as the external script editor in the Preferences (menu: Unity > Preferences and then select the External Tools panel). With this option enabled, Unity will launch MonoDevelop and use it as the default editor for all script files.

##Setting Up the Debugger

To enable MonoDevelop's source level debugging (see below for details) you should firstly check that the _Editor Attaching_ option is enabled in the Preferences on the _External Tools_ panel. Then, you should synchronize the Unity project with the MonoDevelop project (menu: Assets > Open C# Project). Also, make sure that the _Development Build_ and _Script Debugging_ options are enabled in the Build Settings for your target platform (menu: File > Build Settings).

Just before starting a debugging session, select the target you wish to debug from the target list next to the play button (Unity Editor, OSX Player, etc.). You can also select "Attach To Process", this will show the full list of debuggable Unity processes.


![Play button and target list](../uploads/Main/MonoDevelopTargetList.png)


With these steps completed, you are ready to being debugging your Unity scripts by clicking the play button.


##Source Level debugging

The currently open source files are shown as tabs in MonoDevelop and can be edited there with the features of a standard text editor. However, there is also a grey _breakpoint bar_ to the left of the editor panel. Clicking in this bar will add a so-called __breakpoint__ marker next to the line of code.

![Breakpoint being added to code on line 16](../uploads/Main/MonoDevelopBreakpoint.png)

Adding a breakpoint to a line instructs Unity to pause execution of the script just before it reaches that line during Play mode. When the script is "frozen" like this, you can use  the debugger to determine exactly what the script is doing.

![The arrow shows execution paused at the breakpoint](../uploads/Main/MonoDevelopExecPaused.png)

Information about the state of execution is shown in the tabs at the bottom of the MonoDevelop window when execution is paused at a breakpoint. Perhaps the most important of these is the _Locals_ tab.

![Tab showing variable values](../uploads/Main/MonoDevelopVarPanel.png)

This shows the values of local variables in the function that is currently executing. (A pseudo-local variable called _"this"_ is automatically available in every function without being explicitly defined; it is a reference to the current script instance and so all variables defined in the script can be accessed via "this".) You can use breakpoints in combination with the _Locals_ tab to get a similar effect to adding `print` statements to your code - you can interrogate the values of variables at any point you like. However, you can also edit the variable values in the _Locals_ tab. This can be handy when you find a variable incorrectly set and you would like to see if the problem disappears when the value is set how it should be.

A further useful feature of MonoDevelop is _single stepping_. When execution is paused at a breakpoint, a bar of debugging tools will become available in the top portion of the MonoDevelop window:-

![MonoDevelop stepping tools](../uploads/Main/MonoDevelopDebugBar.png)

The four buttons are known as _Continue_, _Step Over_, _Step In_ and _Step Out_ and can also be accessed as commands on the Run menu. _Continue_ resumes execution until the next breakpoint is encountered. _Step Over_ and _Step In_ both execute one line of code at a time. The difference between the two is that _Step Over_ executes any function calls within the line all at once, while _Step In_ allows the stepwise execution to continue into the function. Since it is common to use _Step In_ accidentally on a function that is known to be correct, _Step Out_ continues execution to the end of the current function and then pauses again in the code that originally called it.

A detailed description of source level debugging techniques is not appropriate here but there are various books and web resources offering wisdom on the subject. Additionally, a little experimentation will help you get a feel for the power of the technique and how you can use it to track down most common types of bugs.