#Script Execution Order Settings

By default, the Awake, OnEnable and Update functions of different scripts are called in the order the scripts are loaded (which is arbitrary). However, it is possible to modify this order using the __Script Execution Order__ settings (menu: __Edit &gt; Project Settings &gt; Script Execution Order__).

![](../uploads/Main/ScriptExecSet.png) 

Scripts can be added to the inspector using the Plus "+" button and dragged to change their relative order. Note that it is possible to drag a script either above or below the __Default Time__ bar; those above will execute ahead of the default time while those below will execute after. The ordering of scripts in the dialog from top to bottom determines their execution order. All scripts not in the dialog execute in the default time slot in arbitrary order.

The numbers shown for each script are the values the scripts are actually ordered by. When a script is dragged to a new position, the number for the script is automatically changed accordingly. When a number is changed, either manually or automatically, it changes the meta file for that script. For this reason it's best if as few of the numbers as possible change when the order is changed. This is why, when possible, only the script that is dragged has its number changed, rather than assigning new numbers to all the scripts.
