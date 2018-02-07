Playstation3: System Notifications
==================================


If you want to process notifications sent from the system to your application you can subscribe a delegate to the [PS3SystemUtility.OnSystemNotification](ScriptRef:PS3SystemUtility.OnSystemNotification.html) property. The notifications can be sent by the System, Pad controllers, Move controllers or the Camera. The list of notification ids are available in the [PS3SystemConstants](ScriptRef:PS3SystemConstants.html) enumeration.

###Example

The following example handles the events when the GUI menu screen of the system software has been opened or closed:



````
using UnityEngine;
using System.Collections;

public class Notifications : MonoBehaviour {
   void OnEnable() {
       PS3SystemUtility.OnSystemNotification += HandlePS3Notification;
   }
   void OnDisable() {
       PS3SystemUtility.OnSystemNotification -= HandlePS3Notification;
   }
   void HandlePS3Notification(uint subsystem, uint index, uint notification, uint status) {
       // handle system menu notices
       if (subsystem == (uint)PS3SystemConstants.System) {
           switch (notification) {
               case (uint)PS3SystemConstants.SystemMenuOpen:
                   Debug.Log("menu opened");
                   break;
               case (uint)PS3SystemConstants.SystemMenuClosed:
                   Debug.Log("menu closed");
                   break;
               default:
                   break;
           }
       }
   }
}

````

System Notifications has a special role to play in the application quit process. For example on PS3 when selecting Quit Game from the PS Button.

## Unity's Role in the Quit Process

When the Unity engine receives an OS Quit message (CELL_SYSUTILS_REQUEST_EXITGAME) it will send a System Notification of ExitgameRequest.

Extending the example above:


````
   void HandlePS3Notification(uint subsystem, uint index, uint notification, uint status) {
       // handle system menu notices
       if (subsystem == (uint)PS3SystemConstants.System) {
           switch (notification) {
               case (uint)PS3SystemConstants.ExitgameRequest:
                   Debug.Log(“REQUEST TO SHUTDOWN!);
                   bQuitting = true; // Use this to know that shutdown has been triggered
                   break;
               default:
                   break;
           }
       }
    }

````

Once you have caught this notification in the script, to assist with successful quitting you should terminate and/or conclude all script activity and processes as soon as possible. 

Unity does not kill developer scripts, threads and processes instantly itself since it has no way of knowing what you are doing at that point. There might be important commerce transactions or network activity taking place, or data may be being written. However, as soon as an ExitgameRequest notification is received from Unity, you should handle it as top priority. 

Be sure to appropriately check for this having occurred throughout your systems. A high level check may be insufficient if lower level coroutines may block for some time. It doesn't need to be instant, but processes cannot continue for many seconds. Loading is a good example of this.